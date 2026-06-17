# Space Apps Earth Data - Wildfire Emergency Response System

A full-stack emergency response application for wildfire monitoring and evacuation planning, built for NASA Space Apps Challenge. The system provides real-time wildfire tracking, safe location routing, emergency management services, and AI-powered air quality predictions using machine learning models trained on local environmental data.

## Features

### Citizen View

- **Real-time Wildfire Tracking**: Live wildfire data from NASA EONET API
- **AI-Powered Air Quality Predictions**: Machine learning models forecast air quality based on local environmental conditions
- **Location Services**: Automatic location detection and city identification
- **Safe Route Planning**: Navigate to computed safe locations away from wildfires
- **Interactive Map**: Dynamic mapping with state boundaries (GA, NC, SC, TN)
- **Emergency Alerts**: Visual wildfire proximity indicators
- **Air Quality Monitoring**: Local air quality data integration and predictions

### EMS (Emergency Management Services) View

- **Wildfire-Only Display**: Focused view showing only active wildfires
- **Help Request Markers**: Simulated emergency calls for assistance
- **Response Coordination**: Visual management of emergency situations
- **Geographic Focus**: Concentrated on southeastern US wildfire zones

## Tech Stack

### Frontend

- **Next.js 15** - React framework with App Router
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **Leaflet** - Interactive mapping library
- **React Components** - Modular UI architecture

### Backend & APIs

- **NASA EONET API** - Real-time natural disaster events
- **Nominatim (OpenStreetMap)** - Reverse geocoding services
- **Google Maps Directions** - Route planning (optional)
- **Mapbox Directions** - Alternative routing service (optional)

### AI/ML Components

- **Python/TensorFlow** - Machine learning model training and inference
- **Keras Models** - Pre-trained air quality prediction models (`.h5` format)
- **Google Gemini AI** - Natural language processing and chat interface
- **Jupyter Notebooks** - Data analysis and model development environment
- **Air Quality Forecasting** - NO₂ prediction models with 10-window time series

### Data Sources

- **NASA Earth Observing System Data** - Wildfire event data
- **PublicaMundi GeoJSON** - US state boundary data
- **OpenAQ API** - Air quality measurements

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- Python 3.8+ (for AI/backend components)
- Git

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-username/space-apps-earth-data.git
   cd space-apps-earth-data
   ```

2. **Frontend Setup**

   ```bash
   cd front-end
   npm install
   ```

3. **Backend Setup**

   ```bash
   cd ../ai
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

4. **Environment Configuration**
   Create `front-end/.env.local`:

   ```env
   NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_google_maps_key
   NEXT_PUBLIC_MAPBOX_TOKEN=your_mapbox_token
   NEXT_PUBLIC_OPENAQ_API_KEY=your_openaq_key
   ```

   Create `ai/.env`:

   ```env
   GEMINI_API_KEY=your_gemini_api_key
   ```

### Running the Application

1. **Start the Frontend**

   ```bash
   cd front-end
   npm run dev
   ```

   Access at: `http://localhost:3000`

2. **Start the Backend** (optional)
   ```bash
   cd ai
   python main.py
   ```

## Usage

### Navigation

- Visit `/map` for the main wildfire monitoring interface
- Use the view selector to switch between "Citizen" and "EMS" modes
- Navigate through the app using the top navigation bar

### Citizen Features

1. **View Your Location**: Automatically placed near wildfire areas (simulated)
2. **Navigate to Safety**: Click the red "Navigate to a safe location" button
3. **Route Display**: See direct route lines and distance/time estimates
4. **Local Information**: View your detected city and proximity alerts

### EMS Features

1. **Wildfire Overview**: Clean view of active wildfire locations only
2. **Emergency Requests**: Red person icons indicate help requests
3. **Response Planning**: Click markers for detailed emergency information

## Project Structure

```
space-apps-earth-data/
├── front-end/                 # Next.js application
│   ├── app/                   # App router pages
│   │   ├── map/              # Main map interface
│   │   ├── chat/             # AI chat feature
│   │   └── api/              # API routes
│   ├── components/           # React components
│   │   ├── region-map.tsx    # Main mapping component
│   │   ├── map-viewer.tsx    # View controller
│   │   └── ui/               # UI components
│   └── lib/                  # Utilities
├── ai/                       # Python AI/ML backend
│   ├── main.py              # AI service entry point
│   ├── gemini_wrapper.py    # Gemini AI integration
│   ├── bridge.py            # AI service bridge
│   ├── config.py            # AI configuration
│   └── requirements.txt     # Python dependencies
├── ai2/                     # ML models and data science
│   ├── aqi_forecaster_model.h5    # Air quality prediction model
│   ├── data_extract.py      # Data extraction utilities
│   ├── data.ipynb          # Data analysis notebook
│   ├── new_stuff.ipynb     # Latest model experiments
│   └── stuff.ipynb         # Additional analysis
├── backend/                 # Additional backend services
│   ├── main.py             # Backend API server
│   └── no2_pred_10_window_newer.keras  # NO₂ prediction model
├── data/                    # Data processing and storage
│   ├── extract_data.py     # Data extraction scripts
│   ├── scratch.py          # Data processing utilities
│   └── tempo_no2_data.csv  # TEMPO NO₂ dataset
└── README.md               # This file
```

## AI/ML Models & Capabilities

### Air Quality Prediction Models

- **AQI Forecaster Model** (`aqi_forecaster_model.h5`): TensorFlow/Keras model for predicting Air Quality Index based on environmental conditions
- **NO₂ Prediction Model** (`no2_pred_10_window_newer.keras`): Advanced time-series model using 10-window analysis for nitrogen dioxide concentration forecasting
- **TEMPO NO₂ Integration**: Utilizes NASA TEMPO satellite data for ground-truth NO₂ measurements

### Model Features

- **Time Series Forecasting**: Multi-step ahead predictions for air quality metrics
- **Environmental Data Integration**: Incorporates meteorological and geographical factors
- **Real-time Inference**: Models optimized for low-latency predictions in emergency scenarios
- **Local Air Quality Focus**: Specialized for southeastern US environmental conditions

### AI-Powered Chat Interface

- **Gemini AI Integration**: Natural language processing for emergency response queries
- **Contextual Assistance**: AI chat helps users understand air quality data and evacuation recommendations
- **Emergency Guidance**: Provides personalized safety recommendations based on current conditions

### Data Science Notebooks

- **Data Analysis** (`data.ipynb`): Exploratory data analysis of air quality patterns
- **Model Experiments** (`new_stuff.ipynb`): Latest model training and validation experiments
- **Research Documentation** (`stuff.ipynb`): Additional analysis and feature engineering

### Data Pipeline

- **TEMPO NO₂ Dataset**: Satellite-derived nitrogen dioxide measurements for model training
- **Data Extraction**: Automated pipelines for processing environmental sensor data
- **Feature Engineering**: Advanced preprocessing for time-series and geospatial data

## 🔧 API Integrations

### NASA EONET API

- **Endpoint**: `https://eonet.gsfc.nasa.gov/api/v3/events`
- **Purpose**: Real-time wildfire and natural disaster events
- **Rate Limits**: Public API, no key required

### Reverse Geocoding

- **Service**: Nominatim (OpenStreetMap)
- **Purpose**: Convert coordinates to city names
- **Usage**: Automatic location identification

### Optional Routing Services

- **Google Maps Directions**: Premium routing with traffic data
- **Mapbox Directions**: Alternative routing service
- **Configuration**: Set API keys in environment variables

## Development

### Adding New Features

1. Create feature branches: `git checkout -b feature/your-feature`
2. Frontend components go in `front-end/components/`
3. New pages use Next.js App Router in `front-end/app/`
4. Follow TypeScript conventions and include proper typing

### Testing

```bash
# Frontend
cd front-end
npm run build
npm run lint

# Backend
cd ai
python test_env.py
```

Built for NASA Space Apps Challenge 2025
