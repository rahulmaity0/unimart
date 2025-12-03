# UniMart - University Ecommerce Platform

A modern ecommerce platform built specifically for university students to buy, sell, and trade campus goods and services.

## Features

- **Authentication System**
  - Email/Password login and signup
  - Google OAuth integration
  - Apple OAuth integration
  - User account management

- **User Dashboard**
  - Order management
  - Wishlist
  - Account settings

- **Responsive Design**
  - Mobile-friendly interface
  - Modern UI with Tailwind CSS
  - Smooth animations and transitions

## Tech Stack

- **Frontend**: Next.js 15, React, TypeScript, Tailwind CSS
- **Authentication**: NextAuth.js
- **Deployment Ready**: Optimized for Vercel

## Getting Started

### Prerequisites

- Node.js 18.12.1 or higher
- npm 8.19.2 or higher

### Installation

1. **Clone the repository** (if applicable)
   ```bash
   git clone <repository-url>
   cd unimart-ecommerce
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   - Copy `.env.local.example` to `.env.local`
   - Update with your credentials:
   ```bash
   cp .env.local.example .env.local
   ```

### Configuring OAuth Providers

#### Google OAuth Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable Google+ API
4. Create OAuth 2.0 credentials (Web application)
5. Add authorized redirect URI: `http://localhost:3000/api/auth/callback/google`
6. Copy Client ID and Client Secret to `.env.local`:
   ```
   GOOGLE_CLIENT_ID=your-client-id
   GOOGLE_CLIENT_SECRET=your-client-secret
   ```

#### Apple OAuth Setup

1. Go to [Apple Developer Portal](https://developer.apple.com/)
2. Create a new App ID
3. Configure "Sign in with Apple" capability
4. Create a Service ID
5. Create a private key for your Service ID
6. Add the following to `.env.local`:
   ```
   APPLE_CLIENT_ID=your-service-id
   APPLE_TEAM_ID=your-team-id
   APPLE_KEY_ID=your-key-id
   APPLE_PRIVATE_KEY=your-private-key
   ```

### Running the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Available Routes

- `/` - Home page
- `/auth/login` - Login page with OAuth options
- `/auth/signup` - Sign up page
- `/dashboard` - User dashboard (requires authentication)
- `/api/auth/...` - NextAuth API routes

## Project Structure

```
src/
├── app/
│   ├── api/
│   │   └── auth/[...nextauth]/route.ts  - NextAuth configuration
│   ├── auth/
│   │   ├── login/page.tsx                - Login page
│   │   └── signup/page.tsx               - Sign up page
│   ├── dashboard/
│   │   └── page.tsx                      - User dashboard
│   ├── layout.tsx                        - Root layout with SessionProvider
│   ├── providers.tsx                     - NextAuth SessionProvider wrapper
│   └── globals.css                       - Global styles
├── .env.local                             - Environment variables (not in git)
├── .env.local.example                     - Template for environment variables
├── next.config.ts                         - Next.js configuration
├── tailwind.config.ts                     - Tailwind CSS configuration
├── tsconfig.json                          - TypeScript configuration
└── package.json                           - Dependencies and scripts
```

## Building for Production

```bash
npm run build
npm start
```

## Environment Variables Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `NEXTAUTH_URL` | Application URL | `http://localhost:3000` |
| `NEXTAUTH_SECRET` | Secret for JWT encryption | Any secure random string |
| `GOOGLE_CLIENT_ID` | Google OAuth Client ID | From Google Cloud Console |
| `GOOGLE_CLIENT_SECRET` | Google OAuth Client Secret | From Google Cloud Console |
| `APPLE_CLIENT_ID` | Apple Service ID | From Apple Developer |
| `APPLE_TEAM_ID` | Apple Team ID | From Apple Developer |
| `APPLE_KEY_ID` | Apple Key ID | From Apple Developer |
| `APPLE_PRIVATE_KEY` | Apple Private Key | From Apple Developer |

## Next Steps

1. **Set up database** - Configure a database (PostgreSQL recommended) for storing user data
2. **Create product catalog** - Build product listing and detail pages
3. **Implement shopping cart** - Add cart functionality
4. **Add payment integration** - Integrate Stripe or PayPal
5. **User profile management** - Enhance user account management
6. **Search and filtering** - Add product search and filtering
7. **Reviews and ratings** - Add product review system
8. **Notifications** - Email and push notifications

## Troubleshooting

### Port 3000 already in use
```bash
npm run dev -- -p 3001
```

### Node version warning
Update Node.js to version 20.9.0 or higher for better compatibility.

### OAuth not working
- Verify environment variables are set correctly
- Check redirect URIs match your OAuth provider settings
- Ensure `NEXTAUTH_SECRET` is set and consistent

## Contributing

Contributions are welcome! Please follow these guidelines:
1. Create a new branch for your feature
2. Commit your changes with clear messages
3. Push to the branch
4. Create a Pull Request

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or feature requests, please create an issue in the repository.

---

Built with ❤️ for university students
