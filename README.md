# tanstack-start-architecture

# Domain-Driven TanStack Start Starter Kit

This repository skeleton demonstrates an enterprise-grade Domain-Driven Design architecture using TanStack Start with React 19. Use it as a foundation for your next large-scale project.

---

## 📁 Repository Structure
```plaintext
my-enterprise-app/
├── README.md
├── package.json
├── tsconfig.json
├── .eslintrc.js
├── .prettierrc
├── src/
│   ├── app/
│   │   ├── routes/
│   │   │   ├── (auth)/
│   │   │   │   ├── login.tsx
│   │   │   │   └── register.tsx
│   │   │   ├── (dashboard)/
│   │   │   │   ├── index.tsx
│   │   │   │   └── settings/
│   │   │   │       └── profile.tsx
│   │   │   ├── (admin)/
│   │   │   │   ├── index.tsx
│   │   │   │   └── users.tsx
│   │   │   └── _layout.tsx
│   │   ├── routeTree.tsx
│   │   └── router.tsx
│   ├── modules/
│   │   ├── auth/
│   │   │   ├── api/auth.api.ts
│   │   │   ├── components/LoginForm.tsx
│   │   │   ├── components/RegisterForm.tsx
│   │   │   ├── hooks/useLogin.ts
│   │   │   ├── hooks/useRegister.ts
│   │   │   ├── services/AuthService.ts
│   │   │   ├── validation/authSchemas.ts
│   │   │   └── types/auth.types.ts
│   │   └── posts/   (copy same structure as auth)
│   ├── shared/
│   │   ├── ui/
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   └── Modal.tsx
│   │   ├── components/
│   │   │   ├── Table.tsx
│   │   │   └── Avatar.tsx
│   │   ├── hooks/useDebounce.ts
│   │   ├── services/LoggerService.ts
│   │   ├── context/AuthContext.tsx
│   │   └── lib/apiClient.ts
│   ├── providers/
│   │   └── AppProviders.tsx
│   ├── styles/
│   │   └── globals.css
│   └── index.tsx
├── public/
│   └── favicon.ico
└── turbo.json      (for monorepo/Turborepo support)
```

---

## 🔧 Sample Files

### package.json
```json
{
  "name": "my-enterprise-app",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "start dev",
    "build": "start build",
    "preview": "start preview",
    "lint": "eslint . --ext .ts,.tsx",
    "format": "prettier --write ."
  },
  "dependencies": {
    "@tanstack/react-query": "^5.0.0",
    "@tanstack/react-location": "^1.0.0",
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "zod": "^4.0.0"
  },
  "devDependencies": {
    "typescript": "^5.0.0",
    "eslint": "^8.0.0",
    "prettier": "^2.0.0"
  }
}
```

---

### src/app/router.tsx
```tsx
import { createRouter, rootRoute } from '@tanstack/react-location';
import { routeTree } from './routeTree';

export const router = createRouter({
  routeTree: rootRoute.addChildren(routeTree),
});
```

---

### src/app/routeTree.tsx
```tsx
import { Route } from '@tanstack/react-location';

export const routeTree: Route[] = [
  {
    id: 'login',
    path: '/login',
    element: <LoginPage />,
  },
  {
    id: 'dashboard',
    path: '/',
    element: <DashboardLayout />,
    children: [
      { path: '/', element: <HomePage /> },
      { path: 'settings/profile', element: <ProfilePage /> },
    ],
  },
  // ...admin, etc.
];
```

---

### src/modules/auth/services/AuthService.ts
```ts
export class AuthService {
  static async login(email: string, password: string) {
    const res = await apiClient.post('/auth/login', { email, password });
    return res.data;
  }

  static async register(data: RegisterPayload) {
    const res = await apiClient.post('/auth/register', data);
    return res.data;
  }
}
```

---

### src/shared/ui/Button.tsx
```tsx
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {}
export const Button: React.FC<ButtonProps> = ({ children, ...props }) => (
  <button className="px-4 py-2 rounded bg-blue-600 text-white" {...props}>
    {children}
  </button>
);
```

---

## 🚀 Getting Started
1. **Clone** this starter:  
   ```bash
   git clone https://github.com/your-org/my-enterprise-app.git
   cd my-enterprise-app
   npm install
   npm run dev
   ```
2. **Develop:** Build your modules under `src/modules`, share UI in `src/shared/ui`, and define routes in `src/app/routes`.
3. **Deploy:** Use Vercel, AWS Amplify, or your preferred platform.

---

Use this as a **solid foundation** for any large-scale, domain-driven React 19 + TanStack Start project! Modify and expand it to match your business domains and teams’ needs.

