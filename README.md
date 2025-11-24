# Mangoma - Music Streaming Platform

A full-stack Spotify-inspired music streaming web application built with Next.js 13, Supabase, and Stripe. Users can upload, discover, and stream music with a modern, responsive interface.

![Next.js](https://img.shields.io/badge/Next.js-13.4-black?style=flat-square&logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.1-blue?style=flat-square&logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.3-38B2AC?style=flat-square&logo=tailwind-css)
![Supabase](https://img.shields.io/badge/Supabase-Backend-3ECF8E?style=flat-square&logo=supabase)
![Stripe](https://img.shields.io/badge/Stripe-Payments-635BFF?style=flat-square&logo=stripe)

## Features

- **User Authentication** - Secure login with GitHub OAuth and magic link authentication via Supabase
- **Music Upload** - Upload songs with cover images directly to cloud storage
- **Music Player** - Full-featured player with play/pause, next/previous, volume control, and progress tracking
- **Search** - Real-time debounced search to find songs by title
- **Favorites** - Like songs and access your personalized liked songs playlist
- **Personal Library** - View and manage your uploaded songs
- **Responsive Design** - Seamless experience across desktop, tablet, and mobile devices
- **Subscription System** - Stripe integration for premium subscriptions

## Tech Stack

### Frontend
- **Next.js 13** - React framework with App Router and Server Components
- **React 18** - UI library with hooks
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **Radix UI** - Accessible component primitives
- **Zustand** - Lightweight state management

### Backend
- **Supabase** - PostgreSQL database, authentication, and file storage
- **Stripe** - Payment processing and subscription management

### Libraries
- **React Hook Form** - Form validation and handling
- **use-sound** - Audio playback
- **react-hot-toast** - Toast notifications
- **react-icons** - Icon library

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Next.js App Router                        │
├─────────────────────────────────────────────────────────────────┤
│  Server Components          │         Client Components          │
│  ─────────────────          │         ─────────────────          │
│  • Page layouts             │         • Player controls          │
│  • Data fetching            │         • Modals (Auth, Upload)    │
│  • Server actions           │         • Interactive UI           │
├─────────────────────────────────────────────────────────────────┤
│                      State Management                            │
│         Zustand (Player) + React Context (User/Modals)          │
├─────────────────────────────────────────────────────────────────┤
│                         Supabase                                 │
│    ┌──────────────┬──────────────┬──────────────┐              │
│    │     Auth     │   Database   │   Storage    │              │
│    │  (OAuth/JWT) │ (PostgreSQL) │   (Files)    │              │
│    └──────────────┴──────────────┴──────────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

## Project Structure

```
├── app/                    # Next.js App Router
│   ├── (site)/            # Home page route group
│   ├── search/            # Search page
│   ├── liked/             # Liked songs page
│   └── layout.tsx         # Root layout with providers
├── components/            # Reusable UI components
│   ├── Player.tsx         # Music player
│   ├── Sidebar.tsx        # Navigation sidebar
│   ├── AuthModal.tsx      # Authentication modal
│   └── UploadModal.tsx    # Song upload modal
├── hooks/                 # Custom React hooks
│   ├── usePlayer.ts       # Player state management
│   ├── useUser.tsx        # User authentication state
│   └── useOnPlay.ts       # Play song logic
├── actions/               # Server actions for data fetching
├── providers/             # Context providers
├── types.ts               # TypeScript interfaces
└── types_db.ts            # Database schema types
```

## Getting Started

### Prerequisites

- Node.js 16+
- Supabase account
- Stripe account (for payments)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/mangoma.git
   cd mangoma
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**

   Create a `.env.local` file in the root directory:
   ```env
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key
   STRIPE_SECRET_KEY=your_stripe_secret_key
   STRIPE_WEBHOOK_SECRET=your_webhook_secret
   ```

4. **Set up Supabase**

   Create the following tables in your Supabase project:
   - `songs` - Store song metadata
   - `liked_songs` - Track user favorites
   - `users` - Extended user profiles
   - `products`, `prices`, `subscriptions`, `customers` - Stripe integration

5. **Run the development server**
   ```bash
   npm run dev
   ```

6. **Open your browser**

   Navigate to [http://localhost:3000](http://localhost:3000)

### Build for Production

```bash
npm run build
npm start
```

## Database Schema

| Table | Description |
|-------|-------------|
| `songs` | Song metadata (title, author, file paths) |
| `liked_songs` | Junction table for user favorites |
| `users` | Extended user profile information |
| `subscriptions` | Stripe subscription records |
| `customers` | Stripe customer mapping |
| `products` | Available subscription products |
| `prices` | Pricing tiers |

## Key Implementation Details

### Server Components
Leverages Next.js 13 Server Components for optimal performance - data fetching happens on the server, reducing client-side JavaScript bundle size.

### Real-time Search
Implements debounced search (500ms delay) to minimize API calls while providing responsive search results.

### Audio Playback
Uses the `use-sound` library for audio playback with support for play/pause, volume control, and track progression.

### Authentication Flow
Supabase Auth with GitHub OAuth provider and magic link authentication, integrated with Next.js middleware for protected routes.

## Future Enhancements

- [ ] Playlist creation and management
- [ ] Artist profiles and pages
- [ ] Album support
- [ ] Social features (follow artists, share songs)
- [ ] Audio visualization
- [ ] Offline mode with PWA support
- [ ] Song recommendations

## License

This project is open source and available under the [MIT License](LICENSE).

---

Built with Next.js and Supabase
