# Supabase Setup Guide

## Quick Setup

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Get Your Supabase Credentials

1. Go to your Supabase project dashboard: https://app.supabase.com
2. Navigate to **Settings** → **API**
3. Copy:
   - **Project URL** (this is your `SUPABASE_URL`)
   - **anon/public key** (this is your `SUPABASE_KEY`)

### 3. Configure Credentials

**Option A: Using .env file (Recommended)**
Create a `.env` file in the project root:
```
SUPABASE_URL=https://your-project-id.supabase.co
SUPABASE_KEY=your-anon-key-here
```

**Option B: Direct configuration**
Edit `main.py` and replace:
```python
SUPABASE_URL = 'YOUR_SUPABASE_URL'
SUPABASE_KEY = 'YOUR_SUPABASE_KEY'
```
with your actual credentials.

### 4. Create Required Tables in Supabase

The application expects these tables:

#### `doctors` table:
```sql
CREATE TABLE doctors (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  specialization TEXT,
  qualifications TEXT,
  experience TEXT,
  phone TEXT,
  email TEXT,
  hospital TEXT,
  available_days TEXT[],
  available_times TEXT[],
  consultation_fee INTEGER,
  emergency_available BOOLEAN,
  rating FLOAT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

#### `diseases` table:
```sql
CREATE TABLE diseases (
  id SERIAL PRIMARY KEY,
  name TEXT UNIQUE NOT NULL,
  symptoms TEXT[],
  description TEXT,
  treatment TEXT,
  severity TEXT,
  duration TEXT,
  emergency BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### 5. Test the Connection

Run the application:
```bash
python main.py
```

You should see:
- ✅ Supabase connected successfully (if credentials are correct)
- ⚠️ Supabase credentials not configured (if using placeholders)

## Troubleshooting

### "Supabase library not installed"
```bash
pip install supabase
```

### "Connection test failed"
- Verify your credentials are correct
- Check that the tables exist in your Supabase project
- Ensure your Supabase project is active

### "UnicodeEncodeError" (Windows)
This should be automatically fixed in the code. If you still see this error, ensure you're using Python 3.7+.

