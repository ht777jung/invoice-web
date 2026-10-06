# ModernStarter - 모던 웹 스타터킷

Next.js 16, React 19, TypeScript, Tailwind CSS, shadcn/ui로 구성된 프로덕션 레디 웹 스타터킷입니다.

## 기술 스택

- **프레임워크**: Next.js 16 (App Router)
- **UI 라이브러리**: React 19
- **언어**: TypeScript 5
- **스타일링**: Tailwind CSS v4
- **컴포넌트**: shadcn/ui (base-nova 스타일)
- **폼 관리**: React Hook Form + Zod
- **다크모드**: next-themes
- **토스트**: Sonner
- **아이콘**: Lucide React

## 프로젝트 구조

```
app/
├─ layout.tsx                          # 루트 레이아웃
├─ loading.tsx / error.tsx / not-found.tsx  # 전역 상태 화면
├─ (marketing)/                        # 마케팅 페이지
│  ├─ layout.tsx
│  ├─ page.tsx                         # 랜딩 페이지
│  └─ about/page.tsx
├─ (auth)/                             # 인증 페이지
│  └─ login/page.tsx
└─ (dashboard)/                        # 대시보드
   └─ dashboard/page.tsx

components/
├─ ui/                                 # shadcn/ui 컴포넌트
├─ layout/                             # 레이아웃 블록
├─ shared/                             # 공유 컴포넌트
└─ providers/                          # 글로벌 프로바이더
```

## 설치 및 실행

```bash
# 의존성 설치 (이미 완료됨)
npm install

# 개발 서버 시작
npm run dev

# 타입 체크
npm run typecheck

# 빌드
npm run build

# 프로덕션 실행
npm start
```

개발 서버는 `http://localhost:3000`에서 실행됩니다.

## 사용 가능한 라우트

- `/` - 랜딩 페이지
- `/about` - 소개 페이지
- `/login` - 로그인 페이지 (폼 예제)
- `/dashboard` - 대시보드 메인
- `/*` - 404 Not Found

## 설치된 shadcn/ui 컴포넌트

**P0 (기초)**
- button, separator, skeleton, sheet, dropdown-menu, sonner

**P1 (레이아웃)**
- sidebar, breadcrumb, avatar, tooltip, input

**P2 (콘텐츠)**
- card, label, textarea, checkbox, badge

## 새로운 컴포넌트 추가

```bash
npx shadcn@latest add <component-name>
```

추천: dialog, tabs, table, accordion, select, form, popover, command, calendar

## 다크모드

`next-themes`로 관리되며, ThemeToggle 컴포넌트로 전환할 수 있습니다.

## 폼 예제

React Hook Form + Zod 사용:

```typescript
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

const schema = z.object({
  email: z.string().email(),
  name: z.string().min(2),
});

type FormData = z.infer<typeof schema>;

export function MyForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<FormData>({
    resolver: zodResolver(schema),
  });

  return (
    <form onSubmit={handleSubmit((data) => console.log(data))}>
      <input {...register("name")} />
      {errors.name && <span>{errors.name.message}</span>}
    </form>
  );
}
```

## 토스트 알림

Sonner 사용:

```typescript
import { toast } from "sonner";

toast.success("성공!");
toast.error("오류 발생");
toast.loading("로딩 중...");
```

## 배포

### Vercel (권장)
```bash
vercel
```

### Docker
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

## 주요 파일

- `app/layout.tsx` - 루트 레이아웃
- `app/globals.css` - Tailwind + 다크모드 토큰
- `config/site.ts` - 사이트 설정
- `components.json` - shadcn/ui 설정

## 다음 단계

1. **인증** - NextAuth.js 또는 커스텀 구현
2. **데이터베이스** - Prisma + PostgreSQL
3. **상태 관리** - Zustand (필요시)
4. **테스트** - Vitest + React Testing Library
5. **모니터링** - Sentry

---

**Happy Coding! 🚀**
