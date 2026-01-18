import React, { useState, useEffect } from 'react';
import { 
  ChevronRight, 
  ChevronLeft, 
  Clock, 
  Leaf, 
  Award, 
  ChefHat, 
  Home, 
  BookOpen,
  ArrowRight
} from 'lucide-react';

const App = () => {
  const [currentPage, setCurrentPage] = useState('cover');
  const [history, setHistory] = useState(['cover']);

  const navigateTo = (page) => {
    setHistory([...history, page]);
    setCurrentPage(page);
    window.scrollTo(0, 0);
  };

  const goBack = () => {
    if (history.length > 1) {
      const newHistory = [...history];
      newHistory.pop();
      setHistory(newHistory);
      setCurrentPage(newHistory[newHistory.length - 1]);
    } else {
      setCurrentPage('index');
    }
  };

  // Modern UI Colors
  const colors = {
    bg: '#000000',
    surface: '#0a0a0a',
    gold: '#c5a059',
    textMain: '#ffffff',
    textMuted: '#a1a1aa',
    border: '#27272a'
  };

  const recipes = {
    'avocado-toast': {
      category: 'BREAKFAST',
      title: 'Avocado Toast with Poached Egg',
      image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?q=80&w=1200&auto=format&fit=crop',
      time: '15m',
      tags: ['Veg', 'Protein', 'Easy'],
      ingredients: [
        { qty: '2', unit: 'Slices', item: 'Sourdough bread' },
        { qty: '1', unit: 'Large', item: 'Ripe avocado' },
        { qty: '2', unit: 'Large', item: 'Fresh eggs' },
        { qty: '1', unit: 'tsp', item: 'Chili flakes' },
        { qty: '1/2', unit: 'tsp', item: 'Sea salt' },
        { qty: '1', unit: 'tbsp', item: 'Lemon juice' }
      ],
      steps: [
        'Toast the sourdough slices until golden and crisp.',
        'Mash the avocado in a small bowl with lemon juice and salt.',
        'Bring a pot of water to a gentle simmer with a splash of vinegar. Create a vortex and drop the eggs in for 3 minutes.',
        'Spread the avocado mix generously over the toast.',
        'Top with poached eggs and a sprinkle of chili flakes.'
      ]
    },
    'french-onion': {
      category: 'SOUPS',
      title: 'French Onion Soup',
      image: 'https://images.unsplash.com/photo-1547592166-23ac45744acd?q=80&w=1200&auto=format&fit=crop',
      time: '1.5h',
      tags: ['Traditional', 'Slow Cook'],
      ingredients: [
        { qty: '6', unit: 'Large', item: 'Yellow onions, sliced' },
        { qty: '4', unit: 'tbsp', item: 'Unsalted butter' },
        { qty: '1', unit: 'cup', item: 'Dry white wine' },
        { qty: '6', unit: 'cups', item: 'Beef stock' },
        { qty: '1', unit: 'tbsp', item: 'Fresh thyme' },
        { qty: '1', unit: 'block', item: 'Gruyère cheese' }
      ],
      steps: [
        'Caramelize onions in butter over low heat for 45 minutes until deep brown.',
        'Deglaze the pan with white wine, scraping up the browned bits.',
        'Add beef stock and thyme; simmer for another 30 minutes.',
        'Ladle into ramekins, top with a baguette slice and a thick layer of Gruyère.',
        'Broil until the cheese is bubbling and slightly charred.'
      ]
    },
    'mongolian-beef': {
      category: 'DINNER',
      title: 'Mongolian Beef',
      image: 'https://images.unsplash.com/photo-1534939561126-755ecf1588b0?q=80&w=1200&auto=format&fit=crop',
      time: '30m',
      tags: ['High Protein', 'Savory'],
      ingredients: [
        { qty: '1', unit: 'lb', item: 'Flank steak, sliced thin' },
        { qty: '1/4', unit: 'cup', item: 'Cornstarch' },
        { qty: '2', unit: 'tsp', item: 'Ginger, minced' },
        { qty: '1', unit: 'tbsp', item: 'Garlic, minced' },
        { qty: '1/2', unit: 'cup', item: 'Soy sauce' },
        { qty: '1/2', unit: 'cup', item: 'Brown sugar' }
      ],
      steps: [
        'Coat sliced steak in cornstarch and let sit for 10 minutes.',
        'In a small pan, simmer soy sauce, water, and brown sugar until thickened.',
        'Flash fry the beef in hot oil until crispy on the edges.',
        'Toss the fried beef with the ginger, garlic, and prepared sauce.',
        'Serve immediately over steamed rice with green onions.'
      ]
    },
    'mushroom-risotto': {
      category: 'VEGETARIAN',
      title: 'Mushroom Risotto',
      image: 'https://images.unsplash.com/photo-1476124369491-e7addf5db371?q=80&w=1200&auto=format&fit=crop',
      time: '45m',
      tags: ['Veg', 'Gourmet', 'GF'],
      ingredients: [
        { qty: '1.5', unit: 'cups', item: 'Arborio rice' },
        { qty: '1', unit: 'lb', item: 'Mixed mushrooms' },
        { qty: '5', unit: 'cups', item: 'Warm vegetable stock' },
        { qty: '1/2', unit: 'cup', item: 'Parmesan, grated' },
        { qty: '2', unit: 'tbsp', item: 'Truffle oil' }
      ],
      steps: [
        'Sauté mushrooms in butter until golden and set aside.',
        'Toast the rice in the same pan until the edges are translucent.',
        'Add warm stock one ladle at a time, stirring constantly until absorbed.',
        'Once rice is al dente, stir in mushrooms, parmesan, and butter.',
        'Finish with a drizzle of truffle oil.'
      ]
    }
    // Additional recipes would follow this structure
  };

  const categories = {
    'Breakfast': [
      { id: 'avocado-toast', title: 'Avocado Toast', meta: 'Veg • 15m' },
      { id: 'oatmeal', title: 'Oatmeal', meta: 'Vegan • 10m' },
      { id: 'omelette', title: 'Omelette', meta: 'Keto • 12m' },
      { id: 'pancakes', title: 'Pancakes', meta: 'Sweet • 20m' }
    ],
    'Soups': [
      { id: 'french-onion', title: 'French Onion', meta: 'Trad • 1.5h' },
      { id: 'white-bean', title: 'White Bean', meta: 'Veg • 40m' },
      { id: 'broccoli-cheddar', title: 'Broccoli Cheddar', meta: 'Easy • 30m' },
      { id: 'butternut-squash', title: 'Butternut Squash', meta: 'GF • 45m' }
    ],
    'Lunch': [
      { id: 'cutlet-sandwich', title: 'Cutlet Sandwich', meta: 'Protein • 20m' },
      { id: 'kale-salad', title: 'Kale Salad', meta: 'Healthy • 15m' },
      { id: 'polski-obiad', title: 'Polski Obiad', meta: 'Trad • 1h' }
    ],
    'Dinner': [
      { id: 'mongolian-beef', title: 'Mongolian Beef', meta: 'Keto • 30m' },
      { id: 'beef-stew', title: 'Slow Beef Stew', meta: 'Slow • 4h' },
      { id: 'arroz-pollo', title: 'Arroz con Pollo', meta: 'GF • 50m' },
      { id: 'risotto', title: 'Saffron Risotto', meta: 'Veg • 45m' },
      { id: 'bolognese', title: 'Bolognese', meta: 'Trad • 3h' }
    ]
  };

  const CoverPage = () => (
    <div className="relative w-full h-[720px] bg-black overflow-hidden flex items-center justify-center">
      {/* Background with Sketch Overlay */}
      <div 
        className="absolute inset-0 opacity-40 grayscale"
        style={{ 
          backgroundImage: 'url(https://images.unsplash.com/photo-1543353071-873f17a7a088?q=80&w=1600&auto=format&fit=crop)',
          backgroundSize: 'cover'
        }}
      />
      <div className="absolute inset-0 bg-gradient-to-t from-black via-transparent to-black" />
      
      {/* Sketch Overlay Pattern */}
      <div className="absolute inset-0 opacity-10 pointer-events-none" style={{ backgroundImage: 'repeating-linear-gradient(45deg, transparent, transparent 1px, #fff 1px, #fff 2px)' }} />

      <div className="relative z-10 text-center space-y-4">
        <span className="text-[#c5a059] tracking-[0.4em] text-xs font-bold uppercase">Archive Vol. 01</span>
        <h1 className="text-7xl font-serif italic text-white leading-tight">Home Made</h1>
        <p className="text-zinc-500 font-sans tracking-widest uppercase text-[10px] mt-4">The Culinary Collection for the Modern Kitchen</p>
        <button 
          onClick={() => navigateTo('index')}
          className="mt-12 px-8 py-3 border border-zinc-800 hover:border-[#c5a059] transition-all duration-500 group"
        >
          <span className="text-white text-xs tracking-widest flex items-center gap-2">
            OPEN ARCHIVE <ChevronRight size={14} className="group-hover:translate-x-1 transition-transform" />
          </span>
        </button>
      </div>
    </div>
  );

  const IndexPage = () => (
    <div className="w-full min-h-[720px] bg-[#0a0a0a] p-16">
      <div className="max-w-6xl mx-auto">
        <div className="flex justify-between items-end border-b border-zinc-900 pb-8 mb-12">
          <h2 className="text-4xl font-serif italic text-white">Directory</h2>
          <span className="text-[#c5a059] text-[10px] tracking-widest font-bold uppercase">M M X X V</span>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-4 gap-12">
          {Object.entries(categories).map(([cat, items]) => (
            <div key={cat} className="space-y-6">
              <h3 className="text-[#c5a059] text-[10px] tracking-[0.3em] font-bold uppercase">{cat}</h3>
              <ul className="space-y-4">
                {items.map(item => (
                  <li key={item.id} className="group cursor-pointer" onClick={() => navigateTo(item.id)}>
                    <div className="text-white text-sm font-sans group-hover:text-[#c5a059] transition-colors flex items-center justify-between">
                      {item.title}
                      <ArrowRight size={12} className="opacity-0 group-hover:opacity-100 -translate-x-2 group-hover:translate-x-0 transition-all" />
                    </div>
                    <div className="text-zinc-600 text-[10px] font-sans mt-1">{item.meta}</div>
                  </li>
                ))}
              </ul>
            </div>
          ))}
        </div>
      </div>
    </div>
  );

  const RecipePage = ({ id }) => {
    const data = recipes[id] || recipes['avocado-toast']; // Fallback for demo
    
    return (
      <div className="w-full h-[720px] bg-black flex overflow-hidden">
        {/* Visual Half */}
        <div className="w-1/2 h-full relative group">
          <img 
            src={data.image} 
            alt={data.title}
            className="w-full h-full object-cover grayscale-[0.3] brightness-75 group-hover:grayscale-0 transition-all duration-1000"
          />
          <div className="absolute inset-0 bg-gradient-to-r from-transparent to-black/40" />
          
          <button 
            onClick={goBack}
            className="absolute top-8 left-8 p-3 bg-black/50 backdrop-blur-sm border border-white/10 text-white hover:bg-white hover:text-black transition-all"
          >
            <ChevronLeft size={20} />
          </button>
        </div>

        {/* Information Half */}
        <div className="w-1/2 h-full bg-[#0a0a0a] overflow-y-auto custom-scrollbar p-12 lg:p-16 border-l border-zinc-900">
          <div className="space-y-2 mb-8">
            <span className="text-[#c5a059] tracking-[0.3em] text-[10px] font-bold uppercase">{data.category}</span>
            <h2 className="text-4xl lg:text-5xl font-serif italic text-white leading-tight">{data.title}</h2>
          </div>

          {/* Meta Strip */}
          <div className="flex flex-wrap gap-4 mb-12 py-4 border-y border-zinc-900">
            <div className="flex items-center gap-2 px-3 py-1 bg-zinc-900/50 rounded-full border border-zinc-800">
              <Clock size={12} className="text-[#c5a059]" />
              <span className="text-white text-[10px] font-sans font-bold">{data.time}</span>
            </div>
            {data.tags.map(tag => (
              <div key={tag} className="flex items-center gap-2 px-3 py-1 bg-zinc-900/50 rounded-full border border-zinc-800">
                <span className="text-zinc-400 text-[10px] font-sans font-bold tracking-wider">{tag}</span>
              </div>
            ))}
          </div>

          {/* Ingredients Grid */}
          <div className="mb-12">
            <h4 className="text-zinc-600 text-[10px] tracking-[0.2em] font-bold uppercase mb-6">Ingredients</h4>
            <div className="grid grid-cols-1 gap-y-3">
              {data.ingredients.map((ing, idx) => (
                <div key={idx} className="flex items-baseline gap-2 border-b border-zinc-900/50 pb-2">
                  <span className="text-white font-bold font-sans text-sm w-16">{ing.qty} {ing.unit}</span>
                  <span className="text-zinc-400 font-sans text-sm">{ing.item}</span>
                </div>
              ))}
            </div>
          </div>

          {/* Process Block */}
          <div className="mb-8">
            <h4 className="text-zinc-600 text-[10px] tracking-[0.2em] font-bold uppercase mb-8">The Process</h4>
            <div className="space-y-10">
              {data.steps.map((step, idx) => (
                <div key={idx} className="flex gap-6 group">
                  <div className="flex-none">
                    <span className="text-[#c5a059] font-serif italic text-xl">0{idx + 1}</span>
                  </div>
                  <p className="text-zinc-300 font-sans text-sm leading-relaxed pt-1 group-hover:text-white transition-colors">
                    {step}
                  </p>
                </div>
              ))}
            </div>
          </div>

          {/* Bottom Branding */}
          <div className="pt-12 mt-12 border-t border-zinc-900 flex justify-between items-center opacity-30">
            <span className="font-serif italic text-white">Home Made</span>
            <span className="text-[10px] tracking-widest text-zinc-500 uppercase">Archive No. {Math.floor(Math.random() * 9000) + 1000}</span>
          </div>
        </div>
      </div>
    );
  };

  return (
    <div className="min-h-screen bg-black text-white selection:bg-[#c5a059] selection:text-black">
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@1,6..96,400;1,6..96,700&family=Inter:wght@300;400;600;700&display=swap');
        
        body { font-family: 'Inter', sans-serif; }
        .font-serif { font-family: 'Bodoni Moda', serif; }
        
        .custom-scrollbar::-webkit-scrollbar { width: 4px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: transparent; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #18181b; border-radius: 10px; }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #c5a059; }
      `}</style>

      <div className="flex flex-col items-center justify-center min-h-screen p-4 md:p-8">
        <div className="w-full max-w-[1280px] shadow-2xl shadow-black ring-1 ring-zinc-900 rounded-sm overflow-hidden bg-[#0a0a0a]">
          {currentPage === 'cover' && <CoverPage />}
          {currentPage === 'index' && <IndexPage />}
          {!['cover', 'index'].includes(currentPage) && <RecipePage id={currentPage} />}
        </div>
        
        {/* Navigation Bar */}
        <div className="mt-8 flex items-center gap-8">
          <button 
            onClick={() => navigateTo('cover')}
            className={`p-2 transition-colors ${currentPage === 'cover' ? 'text-[#c5a059]' : 'text-zinc-600 hover:text-white'}`}
          >
            <Home size={18} />
          </button>
          <button 
            onClick={() => navigateTo('index')}
            className={`p-2 transition-colors ${currentPage === 'index' ? 'text-[#c5a059]' : 'text-zinc-600 hover:text-white'}`}
          >
            <BookOpen size={18} />
          </button>
        </div>
      </div>
    </div>
  );
};

export default App;
