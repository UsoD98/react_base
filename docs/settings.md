# Vite + React + TypeScript + Tailwind + DaisyUI + lucide-react 프로젝트 설정 가이드

## 1) 절대 경로 설정: `@`

우선 절대 경로 설정을 위해 @types/node 패키지를 개발 의존성으로 설치합니다.
```bash
npm install -D @types/node
```
그리고 Vite 설정 파일인 `vite.config.ts`에서 절대 경로 설정을 추가합니다.
```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'node:path';
import { fileURLToPath } from 'node:url';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(fileURLToPath(new URL('.', import.meta.url)), 'src'),
    },
  },
});
```
또한 TypeScript 설정 파일인 `tsconfig.app.json`에서도 절대 경로 설정
을 추가합니다.
```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    },
    "strict": true,
    "resolveJsonModule": true,
    "ignoreDeprecations": "6.0"
  }
}
```
> 참고 : 앱 코드의 import는 가능한 한 모두 `@/`를 사용합니다. <br/>
> 현재 프로젝트는 `tsconfig.node.json`도 함께 사용하므로 Vite 설정 파일은 해당 설정의 영향을 받습니다.

## 2) 스타일링 셋업: Tailwind v4 + daisyUI + lucide-react
Tailwind CSS와 daisyUI, lucide-react 아이콘 라이브러리를 설치합니다.
```bash
npm install tailwindcss@latest @tailwindcss/vite@latest daisyui@ lucide-react
```
그리고 `src/index.css` 파일에서 Tailwind와 daisyUI를 불러옵니다.
```css
@import "tailwindcss";
@plugin "daisyui";
```

vite.config.ts 파일에서 Tailwind CSS 플러그인을 추가합니다.
```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'node:path';
import { fileURLToPath } from 'node:url';
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  resolve: {
    alias: {
      '@': path.resolve(fileURLToPath(new URL('.', import.meta.url)), 'src'),
    },
  },
});
```
### 확인 포인트
- Tailwind 4버전 환경이므로 기존 `tailwind.config.ts` 파일은 생성하지 않습니다.
- daisyUI는 Tailwind CSS의 플러그인으로, Tailwind 설정 파일이 없어도 기본 스타일이 적용됩니다. 필요에 따라 daisyUI의 테마 설정을 추가할 수 있습니다.
- lucide-react는 아이콘 라이브러리로, 필요한 아이콘을 컴포넌트로 불러와 사용할 수 있습니다.
- 이제 프로젝트에서 절대 경로와 Tailwind CSS, daisyUI, lucide-react를 활용하여 스타일링을 진행할 수 있습니다.

## 3) 진입점 설정
`src/main.tsx` 파일에서 React 애플리케이션의 진입점을 설정합니다.
```tsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import App from '@/App';

createRoot(document.getElementById('root') as HTMLElement).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
이제 프로젝트가 정상적으로 설정되었으며, 절대 경로와 Tailwind CSS, daisyUI, lucide-react를 활용하여 개발을 시작할 수 있습니다.


