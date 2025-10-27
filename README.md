# ADLA-BADLI

ADLA BADLI is a next-generation hybrid trading platform that redefines digital exchange by blending barter, tokenization, and monetary transactions into one secure ecosystem. It enables users to trade products and services seamlessly using SWP Tokens, a blockchain-backed digital currency that ensures transparent and immutable transactions.

A modern, AI-powered trading platform with blockchain-secured transactions, gamification, and real-time messaging.

## 🚀 Features

### ✅ Fully Implemented Backend

1. **Authentication System**
   - User signup and login
   - Profile management
   - KYC verification workflow
   - Session management with Supabase Auth

2. **Marketplace**
   - Listing CRUD operations
   - Advanced filtering and search
   - Category-based browsing
   - AI-powered recommendations
   - Real-time inventory management

3. **Wallet & Transactions**
   - SWP token balance tracking
   - Transaction history
   - Bonus rewards system
   - Swap processing
   - Real-time updates via Supabase subscriptions

4. **Gamification**
   - XP and level system (Trader → Expert → Legend)
   - Achievements and badges
   - Missions with rewards
   - Activity logging
   - Progress tracking

5. **Messaging** (Service Layer Ready)
   - Real-time chat system
   - Conversation management
   - Read receipts
   - Message search

6. **Profile Management**
   - Trust score tracking
   - Trade statistics
   - Rating system
   - Blockchain ID integration

## 🛠️ Tech Stack

- **Frontend**: React 18 + TypeScript + Vite
- **Styling**: TailwindCSS + Framer Motion
- **Backend**: Supabase (PostgreSQL + Auth + Real-time)
- **State Management**: React Context API
- **Icons**: Lucide React

## 📁 Project Structure

```
project/
├── src/
│   ├── components/          # UI Components
│   │   ├── Navigation.tsx   # Nav with auth
│   │   ├── Hero.tsx
│   │   ├── SignUpVerification.tsx  # Auth integration
│   │   ├── SignUpModal.tsx  # Sign up/in modal
│   │   ├── Marketplace.tsx  # Connected to backend
│   │   ├── Wallet.tsx       # Connected to backend
│   │   ├── Gamification.tsx # Connected to backend
│   │   ├── Profile.tsx      # Connected to backend
│   │   ├── ChatCommunity.tsx
│   │   ├── UserChat.tsx
│   │   └── SwapitAI.tsx
│   │
│   ├── contexts/            # Global State Management
│   │   ├── AuthContext.tsx
│   │   ├── WalletContext.tsx
│   │   ├── MarketplaceContext.tsx
│   │   └── AppProviders.tsx
│   │
│   ├── services/            # Backend Service Layer
│   │   ├── authService.ts
│   │   ├── marketplaceService.ts
│   │   ├── walletService.ts
│   │   ├── messagingService.ts
│   │   └── gamificationService.ts
│   │
│   └── lib/
│       └── supabase.ts      # Supabase client config
│
├── supabase-schema.sql      # Complete database schema
└── README.md
```

## 🗄️ Database Schema

The complete database schema includes:

- **profiles** - User profiles with stats, levels, and verification
- **wallet** - User wallets with SWP balance and rewards
- **listings** - Marketplace items with categories and conditions
- **transactions** - Transaction history with status tracking
- **conversations** - Chat conversations between users
- **messages** - Individual chat messages
- **achievements** - User achievements and badges
- **missions** - Gamification missions with rewards
- **activity_log** - User activity tracking

All tables include:
- Row Level Security (RLS) policies
- Automatic timestamps
- Proper indexes for performance
- Foreign key relationships

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ installed
- A Supabase account (free tier works)

### 1. Clone and Install

```bash
cd project
npm install
```

### 2. Set Up Supabase

1. Go to [supabase.com](https://supabase.com) and create a new project
2. Wait for the project to be ready (2-3 minutes)
3. Go to Project Settings → API
4. Copy your Project URL and anon/public key

### 3. Run Database Schema

1. In your Supabase project, go to SQL Editor
2. Open the `supabase-schema.sql` file from the project root
3. Copy and paste the entire contents into the SQL Editor
4. Click "Run" to create all tables, indexes, and policies

### 4. Configure Environment Variables

Create a `.env` file in the `project` directory:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Replace the values with your actual Supabase credentials.

### 5. Run the Development Server

```bash
npm run dev
```

The app will be available at http://localhost:5173

## 🔐 Authentication Flow

1. Click "Sign In" in the navigation
2. Choose "Sign Up" to create a new account
3. Fill in your details (email, password, username, full name)
4. You'll be automatically logged in
5. Your profile, wallet, achievements, and missions are automatically created

### Default Starting Values

- **Wallet Balance**: 1000 SWP
- **Level**: Trader
- **XP**: 0
- **Trust Score**: 0%
- **Total Trades**: 0

## 📊 Service Layer API

### Authentication Service

```typescript
import { authService } from './services/authService';

// Sign up
await authService.signUp({ email, password, username, full_name });

// Sign in
await authService.signIn(email, password);

// Get profile
const profile = await authService.getProfile(userId);

// Update profile
await authService.updateProfile(userId, { location: 'San Francisco' });
```

### Marketplace Service

```typescript
import { marketplaceService } from './services/marketplaceService';

// Get listings with filters
const { data } = await marketplaceService.getListings({
  category: 'Electronics',
  minPrice: 100,
  maxPrice: 1000,
  prime: true
}, 'price_low');

// Get AI suggestions
const suggestions = await marketplaceService.getAISuggestions(userId);

// Search listings
const results = await marketplaceService.searchListings('iPhone');
```

### Wallet Service

```typescript
import { walletService } from './services/walletService';

// Get wallet
const wallet = await walletService.getWallet(userId);

// Add funds
await walletService.addFunds(userId, 500);

// Get transactions
const { data } = await walletService.getTransactions(userId);
```

### Gamification Service

```typescript
import { gamificationService } from './services/gamificationService';

// Get missions
const { data } = await gamificationService.getMissions(userId);

// Add XP
await gamificationService.addXP(userId, 100);

// Award achievement
await gamificationService.awardAchievement(userId, 'First Swap');
```

## 🎮 Using the Context API

The app uses React Context for global state management:

```typescript
import { useAuth } from './contexts/AuthContext';
import { useWallet } from './contexts/WalletContext';
import { useMarketplace } from './contexts/MarketplaceContext';

function MyComponent() {
  const { user, profile, signOut } = useAuth();
  const { wallet, transactions } = useWallet();
  const { listings, loading } = useMarketplace();
  
  // Use the data...
}
```

## 🔄 Real-time Features

The app uses Supabase real-time subscriptions for:

- **Wallet updates** - Balance changes reflect immediately
- **New transactions** - Transaction list updates in real-time
- **Messages** - Chat messages appear instantly (when integrated)

## 🎨 Customization

### Adding New Listings

Listings can be added programmatically or through the service:

```typescript
import { marketplaceService } from './services/marketplaceService';

await marketplaceService.createListing({
  user_id: userId,
  title: 'MacBook Pro 2023',
  description: 'Excellent condition, barely used',
  category: 'Electronics',
  condition: 'Like New',
  swp_value: 1500,
  original_price: 2399,
  image_urls: ['https://example.com/image.jpg'],
  in_stock: true,
  prime: true,
  ai_suggested: false
});
```

### Customizing Levels

Edit the level thresholds in `gamificationService.ts`:

```typescript
const LEVEL_THRESHOLDS = [
  { name: 'Trader', min: 0, max: 999 },
  { name: 'Expert', min: 1000, max: 4999 },
  { name: 'Legend', min: 5000, max: Infinity },
];
```

## 🧪 Testing the Features

### 1. Authentication
- Sign up with a new account
- Check that the profile is created
- Verify you get 1000 SWP starting balance

### 2. Marketplace
- Browse listings
- Use filters and search
- Change sort order

### 3. Wallet
- View your balance (should be 1000 SWP)
- Check the transaction history

### 4. Gamification
- View your missions
- Check achievements
- See your XP progress

### 5. Profile
- View your profile stats
- See achievements and activity
- Check trust score and rating

## 🔒 Security Features

- Row Level Security (RLS) on all tables
- Users can only access their own data
- Secure authentication with Supabase
- API keys are environment variables
- No sensitive data in frontend code

## 📈 Performance Optimizations

- Database indexes on frequently queried columns
- React Context prevents prop drilling
- Lazy loading of data
- Real-time subscriptions reduce polling
- Optimized image loading

## 🐛 Troubleshooting

### Issue: "Invalid API Key"
- Check your `.env` file
- Ensure keys match your Supabase project
- Restart the dev server after changing `.env`

### Issue: Database Errors
- Run the complete SQL schema in Supabase
- Check RLS policies are enabled
- Verify tables were created successfully

### Issue: Authentication Not Working
- Clear browser storage
- Check Supabase Auth settings
- Verify email confirmation is disabled (for testing)

## 🚀 Deployment

### Build for Production

```bash
npm run build
```

### Deploy to Vercel/Netlify

1. Connect your Git repository
2. Set environment variables in the hosting platform
3. Deploy!

### Environment Variables for Production

```
VITE_SUPABASE_URL=your_production_supabase_url
VITE_SUPABASE_ANON_KEY=your_production_supabase_anon_key
```

## 📝 Future Enhancements

Potential features to add:

- [ ] Complete messaging UI integration
- [ ] AI-powered trade recommendations
- [ ] Blockchain wallet integration
- [ ] Push notifications
- [ ] Image upload for listings
- [ ] Advanced analytics dashboard
- [ ] Social features (follow, like, share)
- [ ] Multi-currency support
- [ ] Mobile app (React Native)

## 🤝 Contributing

This is a demo project showcasing a full-stack implementation with Supabase, React, and TypeScript.

## 📄 License

MIT License - feel free to use this as a learning resource or starting point for your own projects!

## 🙏 Acknowledgments

- Built with [Supabase](https://supabase.com)
- UI powered by [TailwindCSS](https://tailwindcss.com)
- Animations by [Framer Motion](https://www.framer.com/motion/)
- Icons from [Lucide](https://lucide.dev)

---

**Note**: This is a demonstration project. For production use, add comprehensive error handling, input validation, rate limiting, and security audits.
