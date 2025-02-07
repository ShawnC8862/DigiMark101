# DigiMark101
Ai Digital Marketing Agency 
import React, { Suspense, lazy, createContext, useContext, useReducer } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Navbar from './components/Navbar';
import Footer from './components/Footer';
import Loading from './components/Loading';
import ShopPage from './pages/ShopPage';
import CustomAIPage from './pages/CustomAIPage';
import PricingPage from './pages/PricingPage';

// Lazy loading pages for optimized performance on Vercel
const HomePage = lazy(() => import('./pages/HomePage'));
const FeaturesPage = lazy(() => import('./pages/FeaturesPage'));
const AppStorePage = lazy(() => import('./pages/AppStorePage'));
const ContactPage = lazy(() => import('./pages/ContactPage'));
const DashboardPage = lazy(() => import('./pages/DashboardPage'));
const AIWebsiteBuilderPage = lazy(() => import('./pages/AIWebsiteBuilderPage'));
const AILogosPage = lazy(() => import('./pages/AILogosPage'));
const TemplatesPage = lazy(() => import('./pages/TemplatesPage'));
const MarketingDashboardPage = lazy(() => import('./pages/MarketingDashboardPage'));
const AIAutomationToolsPage = lazy(() => import('./pages/AIAutomationToolsPage'));

// Context setup for global state management
const initialState = {
  user: null,
  theme: 'light',
};

const reducer = (state, action) => {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    case 'TOGGLE_THEME':
      return { ...state, theme: state.theme === 'light' ? 'dark' : 'light' };
    default:
      return state;
  }
};

export const GlobalContext = createContext();
export const useGlobalContext = () => useContext(GlobalContext);

const App = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <GlobalContext.Provider value={{ state, dispatch }}>
      <Router>
        <Navbar />
        <Suspense fallback={<Loading />}>
          <Routes>
            <Route path="/" element={<HomePage />} />
            <Route path="/features" element={<FeaturesPage />} />
            <Route path="/pricing" element={<PricingPage />} />
            <Route path="/app-store" element={<AppStorePage />} />
            <Route path="/contact" element={<ContactPage />} />
            <Route path="/dashboard" element={<DashboardPage />} />
            <Route path="/ai-website-builder" element={<AIWebsiteBuilderPage />} />
            <Route path="/ai-logos" element={<AILogosPage />} />
            <Route path="/templates" element={<TemplatesPage />} />
            <Route path="/marketing-dashboard" element={<MarketingDashboardPage />} />
            <Route path="/ai-automation-tools" element={<AIAutomationToolsPage />} />
            <Route path="/shop" element={<ShopPage />} />
            <Route path="/custom-ai" element={<CustomAIPage />} />
          </Routes>
        </Suspense>
        <Footer />
      </Router>
    </GlobalContext.Provider>
  );
};

export default App;
