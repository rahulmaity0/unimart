# UniMart Login & Signup Page Components

## 📋 Overview

This document outlines the authentication flows and components built for UniMart.

## 🔐 Authentication Flow

```
User Visits Website
        ↓
    ↙      ↘
LOGIN    SIGNUP
   ↓         ↓
┌─────────────────────────────────────────────────────┐
│  Email/Password  OR  Google OAuth  OR  Apple OAuth   │
└─────────────────────────────────────────────────────┘
        ↓
  ✅ Valid Credentials
        ↓
  Create Session (JWT)
        ↓
  Redirect to Dashboard
        ↓
  Access Protected Pages
```

## 🎨 Login Page Layout

```
┌─────────────────────────────────────────────────┐
│                                                 │
│         ┌──────────────────────────────┐        │
│         │      UniMart                 │        │
│         │  University Ecommerce        │        │
│         └──────────────────────────────┘        │
│                                                 │
│    ┌─────────────────────────────────────┐      │
│    │     LOGIN FORM                      │      │
│    ├─────────────────────────────────────┤      │
│    │ Email:     [________________]        │      │
│    │ Password:  [________________]        │      │
│    │                                     │      │
│    │ ☑ Remember me    [Forgot password?] │      │
│    │                                     │      │
│    │  [Sign In Button ████████████████]  │      │
│    │                                     │      │
│    │    ─────── Or continue with ────    │      │
│    │                                     │      │
│    │  [🔵 Sign in with Google ████████]  │      │
│    │  [🍎 Sign in with Apple █████████]  │      │
│    │                                     │      │
│    │  Don't have account? Create one     │      │
│    └─────────────────────────────────────┘      │
│                                                 │
│         [Back to home]                         │
└─────────────────────────────────────────────────┘
```

## 🎨 Signup Page Layout

```
┌─────────────────────────────────────────────────┐
│                                                 │
│         ┌──────────────────────────────┐        │
│         │      UniMart                 │        │
│         │  University Ecommerce        │        │
│         └──────────────────────────────┘        │
│                                                 │
│    ┌─────────────────────────────────────┐      │
│    │     CREATE ACCOUNT                  │      │
│    ├─────────────────────────────────────┤      │
│    │ Full Name:  [________________]       │      │
│    │ Email:      [________________]       │      │
│    │ University: [▼ Select university]    │      │
│    │ Password:   [________________]       │      │
│    │             (8+ characters)         │      │
│    │ Confirm:    [________________]       │      │
│    │                                     │      │
│    │ ☑ I agree to Terms of Service      │      │
│    │                                     │      │
│    │  [Create Account Button ███████]    │      │
│    │                                     │      │
│    │    ─────── Or sign up with ────     │      │
│    │                                     │      │
│    │  [🔵 Sign up with Google ████████]  │      │
│    │  [🍎 Sign up with Apple █████████]  │      │
│    │                                     │      │
│    │  Already have account? Sign in      │      │
│    └─────────────────────────────────────┘      │
│                                                 │
│         [Back to home]                         │
└─────────────────────────────────────────────────┘
```

## 📱 Responsive Design

### Mobile (< 640px)
- Single column layout
- Full-width buttons and inputs
- Touch-friendly button sizes (min 44px height)
- Optimized padding for small screens

### Tablet (640px - 1024px)
- Slightly increased spacing
- Better use of vertical/horizontal space

### Desktop (> 1024px)
- Centered card design
- Optimal reading width
- Full gradient background visible

## 🛠️ Component Architecture

```
/app
├── layout.tsx (Root Layout with SessionProvider)
│   └── Providers
│       └── SessionProvider (from NextAuth)
│
├── /auth
│   ├── /login
│   │   └── page.tsx (Login Component)
│   │       ├── Email form
│   │       ├── OAuth buttons (Google, Apple)
│   │       └── Links (signup, forgot password)
│   │
│   └── /signup
│       └── page.tsx (Signup Component)
│           ├── User registration form
│           ├── OAuth buttons
│           └── Link to login
│
├── /dashboard
│   └── page.tsx (Protected Dashboard)
│       ├── User greeting
│       ├── Stats cards
│       └── Sign out button
│
└── /api/auth
    └── /[...nextauth]
        └── route.ts (NextAuth Configuration)
            ├── Google OAuth Provider
            ├── Apple OAuth Provider
            ├── JWT Callbacks
            └── Session Callbacks
```

## 🔐 Security Features

### Authentication
✅ Session-based authentication with JWT  
✅ Secure password storage (hash with NextAuth)  
✅ OAuth 2.0 flows for social providers  
✅ CSRF protection built into NextAuth  

### Data Protection
✅ Protected routes (redirect to login if not authenticated)  
✅ Session validation on page load  
✅ Secure cookie handling  

### Input Validation
✅ Email format validation  
✅ Password strength requirements (8+ characters)  
✅ Password confirmation matching  
✅ Required field validation  

## 🎯 User Flows

### Login Flow
1. User navigates to `/auth/login`
2. Enters email and password
3. Form submission triggers sign-in
4. Session created if valid
5. Redirect to `/dashboard`
6. Dashboard displays user info

### OAuth (Google) Flow
1. User clicks "Sign in with Google"
2. Redirected to Google consent screen
3. User approves app access
4. Callback to `/api/auth/callback/google`
5. User session created
6. Redirect to `/dashboard`

### OAuth (Apple) Flow
1. User clicks "Sign in with Apple"
2. Opens Apple authentication dialog
3. User authenticates with Face ID/Touch ID or password
4. Callback to `/api/auth/callback/apple`
5. User session created
6. Redirect to `/dashboard`

### Signup Flow
1. User navigates to `/auth/signup`
2. Fills in registration form
3. Selects university from dropdown
4. Sets password (validates 8+ characters)
5. Confirms password match
6. Agrees to terms
7. Account created
8. Session created (auto sign-in)
9. Redirect to `/dashboard`

## 📊 State Management

### NextAuth Session State
```typescript
{
  user: {
    id: string;
    email: string;
    name: string;
    image?: string;
  },
  expires: string; // ISO date string
}
```

### Form State (Login)
```typescript
{
  email: string;
  password: string;
  error: string;
  isLoading: boolean;
}
```

### Form State (Signup)
```typescript
{
  fullName: string;
  email: string;
  university: string;
  password: string;
  confirmPassword: string;
  error: string;
  isLoading: boolean;
}
```

## 🎨 Styling System

### Color Palette
- **Primary**: Blue (`bg-blue-600`, `text-blue-600`)
- **Secondary**: Gray (`text-gray-600`, `border-gray-300`)
- **Success**: Green (for status indicators)
- **Error**: Red (`bg-red-50`, `text-red-700`)
- **Background**: Light gradient (`from-blue-50 to-indigo-100`)

### Typography
- **Headings**: Bold, large font sizes
- **Body text**: Regular weight for readability
- **Labels**: Small, medium weight
- **Buttons**: Semibold for emphasis

### Spacing
- **Card padding**: 2rem (8 units)
- **Form inputs**: 1rem padding (0.5rem top/bottom, 1rem left/right)
- **Button height**: 0.5rem padding = ~2rem total height
- **Gaps**: 1rem between form elements

## 🔧 NextAuth Configuration

### Providers Configured
1. **Google OAuth**
   - Client ID & Secret from Google Cloud
   - Redirect URI: `/api/auth/callback/google`

2. **Apple OAuth**
   - Service ID, Team ID, Key ID from Apple Developer
   - Private key for signing JWTs
   - Redirect URI: `/api/auth/callback/apple`

### Callbacks
- **JWT callback**: Manages token data
- **Session callback**: Adds user ID to session

### Pages
- Sign in: `/auth/login`
- Error: `/auth/error` (can be created later)

## 📈 Scalability Considerations

### Future Enhancements
- [ ] Email verification
- [ ] Two-factor authentication (2FA)
- [ ] Social sign-in with more providers (GitHub, Facebook, Twitter)
- [ ] Account linking (connect multiple sign-in methods)
- [ ] Password reset flow
- [ ] Account deletion
- [ ] User profile management

### Database Integration
- User model to store registration data
- Session storage (optional, default uses JWT)
- Account linking for OAuth providers
- User preferences and settings

### Additional Features
- Email notifications
- Login activity logging
- Device management
- Security settings
- Profile customization

---

**Note**: This is a foundation. As you add more features (products, orders, payments), you'll extend these authentication pages with additional flows and integrations.
