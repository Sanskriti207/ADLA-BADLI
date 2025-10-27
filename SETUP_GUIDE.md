# Swapit - Quick Setup Guide

## 🎯 Complete Backend Implementation

This project now has a **fully functional backend** with:

✅ **Authentication** - Sign up, login, profile management  
✅ **Database** - Complete PostgreSQL schema with RLS  
✅ **Marketplace** - CRUD operations, filters, search  
✅ **Wallet** - Balance tracking, transactions, rewards  
✅ **Gamification** - XP, levels, missions, achievements  
✅ **Messaging** - Service layer ready for integration  
✅ **Real-time** - Live updates via Supabase subscriptions  

## 📋 Quick Start (5 Minutes)

### Step 1: Install Dependencies
```bash
cd project
npm install
```

### Step 2: Create Supabase Project
1. Go to https://supabase.com
2. Click "New Project"
3. Name it "swapit" or any name you prefer
4. Wait 2-3 minutes for setup

### Step 3: Set Up Database
1. In Supabase dashboard → SQL Editor
2. Copy entire contents of `supabase-schema.sql`
3. Paste and click "Run"
4. Wait ~10 seconds for all tables to be created

### Step 4: Configure Environment
1. In Supabase → Project Settings → API
2. Copy "Project URL" and "anon public" key
3. Create `.env` file in `project/` folder:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

### Step 5: Run the App
```bash
npm run dev
```

Visit http://localhost:5173 🎉

## 🧪 Test the Features

### 1. Sign Up (Required First!)
- Click "Sign In" button in navigation
- Switch to "Sign Up" tab
- Enter: email, password, username, full name
- Click "Create Account"

**What Happens Automatically:**
- ✅ User profile created
- ✅ Wallet created with 1000 SWP
- ✅ Default achievements initialized
- ✅ Starting missions created
- ✅ You're logged in!

### 2. Check Your Profile
- Scroll to the Profile section
- See your stats: Trust Score, Trades, Rating, XP
- View your achievements (some earned, some locked)
- Check recent activity log

### 3. Explore Marketplace
- Browse default listings
- Try category filters (sidebar)
- Use sort dropdown (Featured, Price, etc.)
- See AI-suggested items badge
- Check item conditions and prime status

### 4. View Your Wallet
- Scroll to Wallet section
- See your 1000 SWP starting balance
- View transaction history
- See bonus rewards (0 initially)
- Growth statistics

### 5. Check Gamification
- Scroll to "Level Up Your Trading"
- See your current level: "Trader"
- View XP progress bar (0/1000 XP to Expert)
- Check active missions with progress bars
- See mission rewards

## 🎮 How Everything Works

### Authentication Flow
```
Sign Up → Profile Created → Wallet Created (1000 SWP) 
→ Achievements Initialized → Missions Created → Ready to Trade!
```

### Marketplace Flow
```
Browse → Filter/Search → View Item → Add to Cart 
→ Process Payment (deducts SWP) → Transaction Recorded → XP Gained
```

### Gamification Flow
```
Complete Action → XP Awarded → Level Up? → Missions Progress 
→ Achievements Unlocked → Bonus SWP Rewarded
```

### Wallet Flow
```
Starting Balance: 1000 SWP
↓
Trade Items → SWP Sent/Received
Complete Missions → Bonus SWP
Unlock Achievements → Bonus SWP
↓
Balance Updates in Real-time
```

## 📊 Default Data

After signing up, you'll have:

| Feature | Default Value |
|---------|--------------|
| SWP Balance | 1000 SWP |
| Level | Trader |
| XP | 0 / 1000 |
| Trust Score | 0% |
| Total Trades | 0 |
| Rating | 0.0 |
| Achievements | 8 (none earned yet) |
| Missions | 3 active missions |

## 🔍 Where to Find Things

### In the App UI
- **Navigation Bar** → Sign In/Out, User Menu
- **Hero Section** → Landing page
- **Sign Up/Verification** → KYC workflow
- **Marketplace** → Browse and filter items
- **Gamification** → Levels, XP, Missions
- **Wallet** → Balance and transactions
- **Chat** → Coming soon
- **Profile** → Your stats and activity

### In the Code

**Components** (`src/components/`)
- Connected to backend via Context API
- Real data from Supabase
- Loading and error states

**Services** (`src/services/`)
- `authService.ts` - Authentication
- `marketplaceService.ts` - Listings
- `walletService.ts` - Wallet & transactions
- `gamificationService.ts` - XP, achievements
- `messagingService.ts` - Chat (ready to use)

**Contexts** (`src/contexts/`)
- `AuthContext.tsx` - User & profile
- `WalletContext.tsx` - Balance & transactions
- `MarketplaceContext.tsx` - Listings & filters

**Database** (`supabase-schema.sql`)
- All tables with RLS policies
- Indexes for performance
- Triggers for automation

## 🛠️ Customization Tips

### Add Your Own Listings
```typescript
// In your component or service
import { marketplaceService } from './services/marketplaceService';

await marketplaceService.createListing({
  user_id: user.id,
  title: 'Your Item Name',
  description: 'Description here',
  category: 'Electronics', // or other categories
  condition: 'Like New',
  swp_value: 500,
  original_price: 750,
  image_urls: ['https://your-image-url.jpg'],
  in_stock: true,
  prime: true,
  ai_suggested: false
});
```

### Award Custom Achievements
```typescript
import { gamificationService } from './services/gamificationService';

await gamificationService.awardAchievement(userId, 'First Swap');
```

### Add Funds to Wallet
```typescript
import { walletService } from './services/walletService';

await walletService.addFunds(userId, 500); // Add 500 SWP
```

## ⚠️ Common Issues & Solutions

### "Invalid API Key" Error
**Solution**: 
- Check `.env` file exists in `project/` folder
- Verify keys match your Supabase project
- Restart dev server: `Ctrl+C` then `npm run dev`

### Database Tables Not Found
**Solution**:
- Run complete SQL schema in Supabase SQL Editor
- Check for any error messages
- Ensure all tables show up in Table Editor

### Can't Sign Up
**Solution**:
- Disable email confirmation in Supabase: 
  - Authentication → Settings → Email Auth
  - Turn off "Enable email confirmations"

### Marketplace Shows No Items
**Solution**:
- Default items will show even without backend
- Create listings using the service layer
- Check RLS policies are set up correctly

## 🎨 Styling & Design

The app uses:
- **TailwindCSS** for utility classes
- **Framer Motion** for animations
- **Lucide React** for icons
- **Custom glass-morphism** effects
- **Gradient accents** (teal/cyan theme)

## 📱 Features Demo

Try these workflows:

### 1. Complete Trade Simulation
```
1. Sign up
2. Browse marketplace
3. Click "Add to Cart" on item
4. (In real app: checkout flow)
5. See transaction in Wallet
6. XP awarded
7. Mission progress updated
```

### 2. Level Up Journey
```
1. Start as "Trader" (0 XP)
2. Complete actions → Gain XP
3. Reach 1000 XP → "Expert" level
4. Reach 5000 XP → "Legend" level
5. Unlock achievements along the way
```

### 3. Earn Rewards
```
1. Complete mission → Bonus SWP
2. Unlock achievement → Bonus SWP
3. Complete trade → XP points
4. Build trust score → Better matches
```

## 🚀 Ready for Production?

Before deploying:

- [ ] Add proper error handling
- [ ] Implement input validation
- [ ] Add rate limiting
- [ ] Enable email confirmations
- [ ] Set up proper image hosting
- [ ] Add monitoring/analytics
- [ ] Write comprehensive tests
- [ ] Security audit
- [ ] Performance optimization
- [ ] SEO optimization

## 📚 Learn More

- [Supabase Docs](https://supabase.com/docs)
- [React Context API](https://react.dev/reference/react/useContext)
- [TailwindCSS](https://tailwindcss.com/docs)
- [Framer Motion](https://www.framer.com/motion/)

## 💡 Next Steps

1. **Test all features** - Sign up and explore
2. **Add custom listings** - Populate marketplace
3. **Create missions** - Engage users
4. **Build chat UI** - Use messaging service
5. **Deploy** - Share with the world!

---

**Questions?** Check the main README.md for detailed API documentation.

**Happy Trading! 🎉**

