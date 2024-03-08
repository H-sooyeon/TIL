## 인증

애플리케이션에 인증을 추가하려면 NextAuth.js를 사용할 수 있다.

세션 관리, 로그인 및 로그아웃, 기타 인증 측면과 관련된 많은 복잡성을 추상화해준다. 물론, 이러한 기능을 수동으로 구현할 수 있지만 시간이 많이 걸리고 오류가 발생하기 쉽다.

NextAuth.js는 Next.js 애플리케이션의 인증을 위한 통합 솔루션을 제공하여 프로세스를 단순화한다.

## NextAuth.js 설정

NextAuth.js를 설치한다.

`npm intall next-auth@beta`

다음으로 애플리케이션에 대한 비밀 키를 생성한다. 이 키는 쿠키를 암호화하여 사용자 세션의 보안을 보장하는데 사용된다.

`openssl rand -base64 32`

`.env` 파일에 생성된 키를 `AUTH_SECRET` 변수로 추가해준다.

```tsx
AUTH_SECRET = your - secret - key;
```

프로덕션에서도 인증이 작동하려면 Vercel 프로젝트에서도 환경 변수를 업데이트해야 한다.

[Vercel에 환경 변수 추가하는 방법](https://vercel.com/docs/projects/environment-variables)

페이지 옵션 추가

`auth.config.ts` 객체를 내보내는 `authConfig`파일을 프로젝트 루트에 만든다.

```tsx
import type { NextAuthConfig } from "next-auth";

export const authConfig = {
  pages: {
    signIn: "/login",
  },
};
```

`pages` 옵션을 사용하여 사용자 정의 로그인, 로그아웃 및 오류 페이지에 대한 경로를 지정할 수 있다. 필수는 아니지만 `signIn: '/login'` 이 옵션을 추가하면

NextAuth.js의 기본 페이지가 아닌 사용자 정의 로그인 페이지로 리디렉션된다.

다음으로 아래의 옵션을 추가하여 사용자가 로그인을 하지 않으면 메인 페이지에 엑세스 할 수 없게 한다.

```tsx
import type { NextAuthConfig } from "next-auth";

export const authConfig = {
  pages: {
    signIn: "/login",
  },
  callbacks: {
    authorized({ auth, request: { nextUrl } }) {
      const isLoggedIn = !!auth?.user;
      const isOnDashboard = nextUrl.pathname.startsWith("/dashboard");
      if (isOnDashboard) {
        if (isLoggedIn) return true;
        return false; // Redirect unauthenticated users to login page
      } else if (isLoggedIn) {
        return Response.redirect(new URL("/dashboard", nextUrl));
      }
      return true;
    },
  },
  providers: [], // Add providers with an empty array for now
} satisfies NextAuthConfig;
```

콜백은 Next.js 미들웨어가 `authorized`를 통해 해당 페이지에 엑세스할 수 있는 권한이 있는지 확인하는데 사용된다.

요청이 완료되기 전에 호출되며, 속성이 있는 객체를 반환한다. 속성에는 사용자의 세선이 포함된다.

다음으로, authConfig 객체를 미들웨어 파일에 추가해줘야한다.

루트 경로에 `middleware.ts` 파일을 생성한 후 아래의 코드를 붙여준다.

```tsx
import NextAuth from "next-auth";
import { authConfig } from "./auth.config";

export default NextAuth(authConfig).auth;

export const config = {
  // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
  matcher: ["/((?!api|_next/static|_next/image|.*\\.png$).*)"],
};
```

미들웨어를 사용하면 미들웨어가 인증을 확인할 때까지 보호된 경로가 렌더링을 시작하지 않아 애플리케이션의 보안과 성능이 모두 향상된다는 이점이 있다.

## 비밀번호 해싱

비밀번호를 데이터베이스에 저장하기 전에 해시하는 것이 좋다.
해싱은 비밀번호를 무작위로 나타나는 고정 길이의 문자열로 변환하여 사용자 데이터가 노출되더라도 보안 계층을 제공한다.

사용자의 비밀번호를 데이터베이스에 저장하기 전에 해시하도록 `seed.js` 패키지를 사용한다.

패키지에 대한 별도의 파일을 생성해야 하는데, Next.js 미들웨어에서 사용할 수 없는 Node.js API에 의존하기 때문이다.

```tsx
// /auth.ts
import NextAuth from "next-auth";
import { authConfig } from "./auth.config";

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
});
```

## 자격 증명 공급자 추가

다음으로 NextAuth.js에 대한 `providers` 옵션을 추가해야 한다.

Google 또는 GitHub와 같은 다양한 로그인 옵션을 나열하는 배열이다.

자격 증명 공급자를 사용하면 사용자가 사용자 이름과 비밀번호를 사용하여 로그인할 수 있다.

```tsx
// /auth.ts
import NextAuth from "next-auth";
import { authConfig } from "./auth.config";
import Credentials from "next-auth/providers/credentials";

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [Credentials({})],
});
```

<aside>
✅ 자격 증명 공급자보단 OAuth와 같은 대체 공급자를 사용하는 것이 좋다.

</aside>

## 로그인 기능 추가

`authorize` 함수를 사용하여 인증 논리를 처리할 수 있다.

`zod` 서버 작업과 마찬가지로 사용자가 데이터베이스에 존재하는지 확인하기 전에 이메일과 비밀번호의 유효성을 검사하는데 사용할 수 있다.

```tsx
import NextAuth from "next-auth";
import { authConfig } from "./auth.config";
import Credentials from "next-auth/providers/credentials";
import { z } from "zod";

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [
    Credentials({
      async authorize(credentials) {
        const parsedCredentials = z
          .object({ email: z.string().email(), password: z.string().min(6) })
          .safeParse(credentials);
      },
    }),
  ],
});
```

`getUser` 자격 증명을 확인한 후 데이터베이스에서 사용자를 쿼리하는 새 함수를 만든다.

```tsx
// /auth.ts
import NextAuth from "next-auth";
import Credentials from "next-auth/providers/credentials";
import { authConfig } from "./auth.config";
import { z } from "zod";
import { sql } from "@vercel/postgres";
import type { User } from "@/app/lib/definitions";
import bcrypt from "bcrypt";

async function getUser(email: string): Promise<User | undefined> {
  try {
    const user = await sql<User>`SELECT * FROM users WHERE email=${email}`;
    return user.rows[0];
  } catch (error) {
    console.error("Failed to fetch user:", error);
    throw new Error("Failed to fetch user.");
  }
}

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [
    Credentials({
      async authorize(credentials) {
        const parsedCredentials = z
          .object({ email: z.string().email(), password: z.string().min(6) })
          .safeParse(credentials);

        if (parsedCredentials.success) {
          const { email, password } = parsedCredentials.data;
          const user = await getUser(email);
          if (!user) return null;
        }

        return null;
      },
    }),
  ],
});
```

이후 `[bcrypt.compare](http://bcrypt.compare)` 을 호출하여 사용자가 입력한 비밀번호가 실제 비밀번호와 일치하는지 확인한다.

```tsx
import NextAuth from "next-auth";
import Credentials from "next-auth/providers/credentials";
import { authConfig } from "./auth.config";
import { sql } from "@vercel/postgres";
import { z } from "zod";
import type { User } from "@/app/lib/definitions";
import bcrypt from "bcrypt";

// ...

export const { auth, signIn, signOut } = NextAuth({
  ...authConfig,
  providers: [
    Credentials({
      async authorize(credentials) {
        // ...

        if (parsedCredentials.success) {
          const { email, password } = parsedCredentials.data;
          const user = await getUser(email);
          if (!user) return null;
          const passwordsMatch = await bcrypt.compare(password, user.password);

          if (passwordsMatch) return user;
        }

        console.log("Invalid credentials");
        return null;
      },
    }),
  ],
});
```

## 로그인 양식 제출

인증 로직을 로그인 양식과 연결해야 한다.

```tsx
import { signIn } from "@/auth";
import { AuthError } from "next-auth";

// ...

export async function authenticate(
  prevState: string | undefined,
  formData: FormData
) {
  try {
    await signIn("credentials", formData);
  } catch (error) {
    if (error instanceof AuthError) {
      switch (error.type) {
        case "CredentialsSignin":
          return "Invalid credentials.";
        default:
          return "Something went wrong.";
      }
    }
    throw error;
  }
}
```

NextAuth.js 오류는 https://errors.authjs.dev/ 이곳에서 볼 수 있다.

- 이메일:`user@nextmail.com`
- 비밀번호:`123456`
