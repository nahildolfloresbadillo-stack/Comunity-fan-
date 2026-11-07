# Comunity-fan-
Una pagina de fans para fans, esta pagina busca ser una comunidad sana donde todos puedan pasarla bien 
[Uploading comunity_fan_interactive_writing_reading_platform.tsx…]()
import React, { useState, useEffect, useRef } from 'react';

// --- BANNER COMPONENT WITH CUSTOM HEADER IMAGE LOGO ---
const BannerHeader = () => (
  <div className="w-full relative overflow-hidden bg-slate-950 border-b border-purple-900/50 shadow-2xl">
    <div className="max-w-7xl mx-auto px-4 py-4 sm:py-6 flex flex-col md:flex-row items-center justify-between gap-4">
      {/* Visual Header Image Container */}
      <div className="relative group w-full md:w-auto flex justify-center md:justify-start">
        <div className="absolute -inset-1 bg-gradient-to-r from-red-600 via-purple-600 to-amber-500 rounded-2xl blur opacity-30 group-hover:opacity-75 transition duration-1000"></div>
        <div className="relative rounded-xl overflow-hidden border border-purple-500/30 shadow-2xl bg-black max-w-lg w-full">
          <img 
            src="https://raw.githubusercontent.com/placeholder-fan/assets/main/comunity-fan-header.jpg" 
            alt="COMUNITY FAN Logo Banner" 
            className="w-full h-20 sm:h-24 object-cover object-center transform transition duration-500 hover:scale-105"
            onError={(e) => {
              // Fallback styled visual text logo matching the uploaded banner style
              e.target.style.display = 'none';
              e.target.nextSibling.style.display = 'flex';
            }}
          />
          <div className="hidden h-20 sm:h-24 w-full bg-gradient-to-r from-slate-900 via-purple-950 to-amber-950 items-center justify-center p-3 relative border border-amber-500/30">
            <h1 className="text-3xl sm:text-4xl font-extrabold tracking-widest text-transparent bg-clip-text bg-gradient-to-r from-red-500 via-pink-400 to-amber-300 drop-shadow-[0_2px_10px_rgba(239,68,68,0.8)] uppercase font-mono">
              COMUNITY FAN
            </h1>
          </div>
        </div>
      </div>

      {/* Slogan */}
      <div className="text-center md:text-right">
        <p className="text-xs uppercase tracking-widest text-amber-400 font-semibold">Plataforma Creativa de Fanfiction & Historias</p>
        <p className="text-slate-400 text-xs mt-1">Escribe, decora, lee y apoya a tus autores favoritos</p>
      </div>
    </div>
  </div>
);

// --- SVG ICONS ---
const HeartIcon = ({ className = "w-4 h-4", fill = false }) => (
  <svg className={className} fill={fill ? "currentColor" : "none"} viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.684a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
  </svg>
);

const BookmarkIcon = ({ className = "w-4 h-4", fill = false }) => (
  <svg className={className} fill={fill ? "currentColor" : "none"} viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z" />
  </svg>
);

const SearchIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
  </svg>
);

const PlusIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 4v16m8-8H4" />
  </svg>
);

const GiftIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 8v13m0-13V6a2 2 0 112 2h-2zm0 0V6a2 2 0 10-2 2h2zm-7 4h14M5 12v7a2 2 0 002 2h10a2 2 0 002-2v-7" />
  </svg>
);

const BookOpenIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" />
  </svg>
);

const UserIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
  </svg>
);

const ImageIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
  </svg>
);

const VideoIcon = ({ className = "w-4 h-4" }) => (
  <svg className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
  </svg>
);

// --- INITIAL MOCK DATA STORIES ---
const INITIAL_STORIES = [
  {
    id: 'story-1',
    title: 'Ecos entre el Vacío Estelar',
    author: 'Astra_Writer',
    authorEmail: 'astra@comunityfan.com',
    synopsis: 'Un viaje a través de nebulosas olvidadas donde el destino de dos mundos depende de una promesa antigua.',
    fandom: 'Genshin Impact',
    relationships: ['Xiao/Lumine', 'Slow Burn'],
    warnings: ['Sin Advertencias Relevantes'],
    tags: ['Romance Espacial', 'Magia', 'AU'],
    rating: 'General',
    coverImage: 'https://images.unsplash.com/photo-1506703719100-a0f3a48c0f86?w=600&auto=format&fit=crop&q=80',
    kudos: 1420,
    views: 8900,
    decorations: {
      bgColor: '#0f172a',
      textColor: '#f8fafc',
      fontFamily: 'serif',
      accentColor: '#8b5cf6'
    },
    chapters: [
      {
        id: 'c1',
        title: 'Capítulo 1: El Despertar',
        content: `La nave orbitaba la estrella moribunda. En el silencio del espacio, el brillo violeta reflejaba sus dudas...\n\n¿Acaso el universo recordaba las voces que una vez resonaron aquí?`,
        media: [
          { type: 'image', url: 'https://images.unsplash.com/photo-1451187580459-43490279c0fa?w=800&auto=format&fit=crop&q=80', caption: 'Vista del núcleo estelar' }
        ]
      }
    ]
  },
  {
    id: 'story-2',
    title: 'Sombras en la Academia de Neón',
    author: 'KuroNeko',
    authorEmail: 'kuroneko@comunityfan.com',
    synopsis: 'Secretos cyber-punk y códigos prohibidos amenazan con revelar la verdad detrás del Consejo.',
    fandom: 'Cyberpunk 2077',
    relationships: ['Enemies to Lovers'],
    warnings: ['Violencia Gráfica'],
    tags: ['Cyberpunk', 'Acción', 'Hackers'],
    rating: 'Teen',
    coverImage: 'https://images.unsplash.com/photo-1542751371-adc38448a05e?w=600&auto=format&fit=crop&q=80',
    kudos: 980,
    views: 5400,
    decorations: {
      bgColor: '#09090b',
      textColor: '#e4e4e7',
      fontFamily: 'sans-serif',
      accentColor: '#ec4899'
    },
    chapters: [
      {
        id: 'c1',
        title: 'Capítulo 1: Código Cero',
        content: 'Las luces de neón parpadeaban en la llovizna. La terminal mostró la alerta antes de que las alarmas comenzaran a sonar.',
        media: []
      }
    ]
  }
];

export default function App() {
  // State for Navigation & User Session
  const [activeTab, setActiveTab] = useState('explore'); // 'explore', 'write', 'library', 'donations'
  const [user, setUser] = useState(null); // Firebase-like Auth state: { email, username }
  const [authModalOpen, setAuthModalOpen] = useState(false);
  const [authEmail, setAuthEmail] = useState('');
  const [authPassword, setAuthPassword] = useState('');
  const [authUsername, setAuthUsername] = useState('');
  const [isRegistering, setIsRegistering] = useState(false);

  // Database of Stories & Tags
  const [stories, setStories] = useState(INITIAL_STORIES);
  const [globalTags, setGlobalTags] = useState(['Romance Espacial', 'Magia', 'AU', 'Cyberpunk', 'Acción', 'Hackers', 'Slow Burn', 'Enemies to Lovers']);

  // Filters & Search State
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedTag, setSelectedTag] = useState('');
  const [selectedFandom, setSelectedFandom] = useState('');

  // Reader View State
  const [currentStory, setCurrentStory] = useState(null);
  const [currentChapterIndex, setCurrentChapterIndex] = useState(0);
  const [kudosGiven, setKudosGiven] = useState([]);
  const [bookmarks, setBookmarks] = useState([]);

  // Donation Modal State
  const [donationModalOpen, setDonationModalOpen] = useState(false);
  const [donatingToAuthor, setDonatingToAuthor] = useState(null);
  const [donationAmount, setDonationAmount] = useState('5.00');
  const [donationMessage, setDonationMessage] = useState('');

  // Author Story Editor State
  const [editorStory, setEditorStory] = useState({
    title: '',
    synopsis: '',
    fandom: '',
    relationships: '',
    warnings: 'Sin Advertencias Relevantes',
    tags: '',
    rating: 'General',
    coverImage: null, // File Base64 string
    bgColor: '#0f172a',
    textColor: '#f8fafc',
    fontFamily: 'sans-serif',
    accentColor: '#8b5cf6',
    chapters: [
      {
        title: 'Capítulo 1',
        content: '',
        media: [] // { type: 'image' | 'video', url, file }
      }
    ]
  });

  const [activeEditorChapter, setActiveEditorChapter] = useState(0);
  const editorFileInputRef = useRef(null);
  const chapterMediaInputRef = useRef(null);
  const videoInputRef = useRef(null);
  const [youtubeUrlInput, setYoutubeUrlInput] = useState('');

  // Auto Register Dynamic Tags when new stories are published
  const registerNewTags = (newTagsArray) => {
    setGlobalTags(prev => {
      const updated = new Set([...prev, ...newTagsArray.map(t => t.trim()).filter(Boolean)]);
      return Array.from(updated);
    });
  };

  // --- HANDLERS FOR AUTHENTICATION ---
  const handleAuthSubmit = (e) => {
    e.preventDefault();
    if (!authEmail) return;
    
    // Simulate Firebase Auth Login / Registration
    const newUser = {
      email: authEmail,
      username: authUsername || authEmail.split('@')[0]
    };
    setUser(newUser);
    setAuthModalOpen(false);
    setAuthEmail('');
    setAuthPassword('');
    setAuthUsername('');
  };

  const handleLogout = () => {
    setUser(null);
  };

  // --- HANDLERS FOR BOOKMARKING & KUDOS ---
  const toggleBookmark = (storyId) => {
    setBookmarks(prev => 
      prev.includes(storyId) ? prev.filter(id => id !== storyId) : [...prev, storyId]
    );
  };

  const handleGiveKudos = (storyId) => {
    if (kudosGiven.includes(storyId)) return;
    setKudosGiven(prev => [...prev, storyId]);
    setStories(prev => prev.map(s => s.id === storyId ? { ...s, kudos: s.kudos + 1 } : s));
  };

  // --- STORY CREATION / EDITING HANDLERS ---
  const handleCoverUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
        setEditorStory(prev => ({ ...prev, coverImage: reader.result }));
      };
      reader.readAsDataURL(file);
    }
  };

  const handleChapterImageUpload = (e) => {
    const files = Array.from(e.target.files);
    files.forEach(file => {
      const reader = new FileReader();
      reader.onloadend = () => {
        setEditorStory(prev => {
          const updatedChapters = [...prev.chapters];
          updatedChapters[activeEditorChapter].media.push({
            type: 'image',
            url: reader.result,
            caption: file.name
          });
          return { ...prev, chapters: updatedChapters };
        });
      };
      reader.readAsDataURL(file);
    });
  };

  const handlePasteImage = (e) => {
    const items = (e.clipboardData || e.originalEvent.clipboardData).items;
    for (let item of items) {
      if (item.kind === 'file' && item.type.startsWith('image/')) {
        const file = item.getAsFile();
        const reader = new FileReader();
        reader.onloadend = () => {
          setEditorStory(prev => {
            const updatedChapters = [...prev.chapters];
            updatedChapters[activeEditorChapter].media.push({
              type: 'image',
              url: reader.result,
              caption: 'Imagen pegada'
            });
            return { ...prev, chapters: updatedChapters };
          });
        };
        reader.readAsDataURL(file);
      }
    }
  };

  const handleVideoUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
        setEditorStory(prev => {
          const updatedChapters = [...prev.chapters];
          updatedChapters[activeEditorChapter].media.push({
            type: 'video',
            url: reader.result,
            caption: file.name
          });
          return { ...prev, chapters: updatedChapters };
        });
      };
      reader.readAsDataURL(file);
    }
  };

  const handleAddYoutubeVideo = () => {
    if (!youtubeUrlInput) return;
    let embedUrl = youtubeUrlInput;
    if (youtubeUrlInput.includes('watch?v=')) {
      embedUrl = youtubeUrlInput.replace('watch?v=', 'embed/');
    } else if (youtubeUrlInput.includes('youtu.be/')) {
      embedUrl = youtubeUrlInput.replace('youtu.be/', 'www.youtube.com/embed/');
    }

    setEditorStory(prev => {
      const updatedChapters = [...prev.chapters];
      updatedChapters[activeEditorChapter].media.push({
        type: 'youtube',
        url: embedUrl,
        caption: 'Video de YouTube'
      });
      return { ...prev, chapters: updatedChapters };
    });
    setYoutubeUrlInput('');
  };

  const handlePublishStory = (e) => {
    e.preventDefault();
    if (!user) {
      setAuthModalOpen(true);
      return;
    }
    if (!editorStory.title || !editorStory.synopsis || !editorStory.coverImage) {
      alert('Por favor completa el título, sinopsis y exporta la imagen de portada.');
      return;
    }

    const tagList = editorStory.tags.split(',').map(t => t.trim()).filter(Boolean);
    const relList = editorStory.relationships.split(',').map(r => r.trim()).filter(Boolean);

    registerNewTags(tagList);

    const newStory = {
      id: `story-${Date.now()}`,
      title: editorStory.title,
      author: user.username,
      authorEmail: user.email,
      synopsis: editorStory.synopsis,
      fandom: editorStory.fandom || 'Original Work',
      relationships: relList.length ? relList : ['General'],
      warnings: [editorStory.warnings],
      tags: tagList,
      rating: editorStory.rating,
      coverImage: editorStory.coverImage,
      kudos: 0,
      views: 1,
      decorations: {
        bgColor: editorStory.bgColor,
        textColor: editorStory.textColor,
        fontFamily: editorStory.fontFamily,
        accentColor: editorStory.accentColor
      },
      chapters: editorStory.chapters
    };

    setStories(prev => [newStory, ...prev]);
    setActiveTab('explore');
    // Reset editor
    setEditorStory({
      title: '',
      synopsis: '',
      fandom: '',
      relationships: '',
      warnings: 'Sin Advertencias Relevantes',
      tags: '',
      rating: 'General',
      coverImage: null,
      bgColor: '#0f172a',
      textColor: '#f8fafc',
      fontFamily: 'sans-serif',
      accentColor: '#8b5cf6',
      chapters: [{ title: 'Capítulo 1', content: '', media: [] }]
    });
  };

  // --- FILTERED STORIES ---
  const filteredStories = stories.filter(story => {
    const matchesSearch = story.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
                          story.author.toLowerCase().includes(searchQuery.toLowerCase());
    const matchesTag = !selectedTag || story.tags.includes(selectedTag);
    const matchesFandom = !selectedFandom || story.fandom === selectedFandom;
    return matchesSearch && matchesTag && matchesFandom;
  });

  const fandomOptions = Array.from(new Set(stories.map(s => s.fandom)));

  return (
    <div className="min-h-screen bg-slate-950 text-slate-100 flex flex-col font-sans">
      {/* BANNER COMUNITY FAN */}
      <BannerHeader />

      {/* TOP NAVBAR */}
      <nav className="bg-slate-900 border-b border-purple-900/40 sticky top-0 z-40 backdrop-blur-md bg-opacity-90">
        <div className="max-w-7xl mx-auto px-4 py-3 flex items-center justify-between gap-4">
          
          {/* Navigation Links */}
          <div className="flex items-center space-x-1 sm:space-x-3">
            <button
              onClick={() => { setActiveTab('explore'); setCurrentStory(null); }}
              className={`px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold flex items-center space-x-1.5 transition ${
                activeTab === 'explore' && !currentStory ? 'bg-purple-600 text-white' : 'hover:bg-slate-800 text-slate-300'
              }`}
            >
              <BookOpenIcon className="w-4 h-4" />
              <span>Explorar</span>
            </button>

            <button
              onClick={() => { setActiveTab('library'); setCurrentStory(null); }}
              className={`px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold flex items-center space-x-1.5 transition ${
                activeTab === 'library' ? 'bg-purple-600 text-white' : 'hover:bg-slate-800 text-slate-300'
              }`}
            >
              <BookmarkIcon className="w-4 h-4" fill={activeTab === 'library'} />
              <span>Biblioteca ({bookmarks.length})</span>
            </button>

            <button
              onClick={() => { setActiveTab('write'); setCurrentStory(null); }}
              className={`px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold flex items-center space-x-1.5 transition ${
                activeTab === 'write' ? 'bg-amber-500 text-slate-950 font-bold' : 'hover:bg-slate-800 text-slate-300'
              }`}
            >
              <PlusIcon className="w-4 h-4" />
              <span>Escribir Historia</span>
            </button>
          </div>

          {/* User Profile / Auth */}
          <div className="flex items-center space-x-3">
            {user ? (
              <div className="flex items-center space-x-3">
                <span className="text-xs sm:text-sm font-medium text-amber-300 flex items-center space-x-1">
                  <UserIcon className="w-4 h-4" />
                  <span>{user.username}</span>
                </span>
                <button
                  onClick={handleLogout}
                  className="text-xs px-2.5 py-1 rounded bg-slate-800 hover:bg-slate-700 text-slate-400"
                >
                  Salir
                </button>
              </div>
            ) : (
              <button
                onClick={() => setAuthModalOpen(true)}
                className="px-4 py-1.5 rounded-lg text-xs sm:text-sm font-bold bg-gradient-to-r from-red-600 to-purple-600 hover:from-red-500 hover:to-purple-500 text-white shadow"
              >
                Iniciar Sesión / Registro
              </button>
            )}
          </div>

        </div>
      </nav>

      {/* MAIN CONTAINER */}
      <main className="flex-1 max-w-7xl w-full mx-auto p-4 sm:p-6">

        {/* VIEW: READER MODE */}
        {currentStory ? (
          <div className="max-w-4xl mx-auto space-y-6">
            <button
              onClick={() => setCurrentStory(null)}
              className="text-xs font-semibold px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-lg flex items-center space-x-1"
            >
              <span>← Volver a la lista</span>
            </button>

            {/* DECORATED READING CANVAS */}
            <div 
              className="rounded-2xl p-6 sm:p-10 shadow-2xl border border-slate-800 transition-all"
              style={{
                backgroundColor: currentStory.decorations?.bgColor || '#0f172a',
                color: currentStory.decorations?.textColor || '#f8fafc',
                fontFamily: currentStory.decorations?.fontFamily || 'sans-serif'
              }}
            >
              {/* Cover & Story Details */}
              <div className="flex flex-col md:flex-row gap-6 items-center md:items-start border-b pb-6" style={{ borderColor: `${currentStory.decorations?.accentColor || '#8b5cf6'}40` }}>
                <img 
                  src={currentStory.coverImage} 
                  alt={currentStory.title} 
                  className="w-40 h-56 object-cover rounded-xl shadow-xl border-2"
                  style={{ borderColor: currentStory.decorations?.accentColor || '#8b5cf6' }}
                />
                <div className="flex-1 text-center md:text-left space-y-3">
                  <h1 className="text-3xl font-extrabold" style={{ color: currentStory.decorations?.accentColor || '#8b5cf6' }}>
                    {currentStory.title}
                  </h1>
                  <p className="text-sm opacity-80">Por <strong className="underline">{currentStory.author}</strong></p>

                  <div className="flex flex-wrap justify-center md:justify-start gap-1.5 pt-2">
                    <span className="px-2 py-0.5 rounded text-xs font-bold bg-purple-900/60 text-purple-200">
                      Fandom: {currentStory.fandom}
                    </span>
                    {currentStory.relationships?.map((rel, idx) => (
                      <span key={idx} className="px-2 py-0.5 rounded text-xs font-semibold bg-pink-900/50 text-pink-200">
                        {rel}
                      </span>
                    ))}
                    {currentStory.tags?.map((tag, idx) => (
                      <span key={idx} className="px-2 py-0.5 rounded text-xs bg-slate-800 text-slate-300 border border-slate-700">
                        #{tag}
                      </span>
                    ))}
                  </div>

                  <p className="text-sm pt-2 italic leading-relaxed">{currentStory.synopsis}</p>

                  {/* Actions Bar */}
                  <div className="pt-4 flex items-center justify-center md:justify-start gap-3">
                    <button
                      onClick={() => handleGiveKudos(currentStory.id)}
                      className={`px-4 py-2 rounded-xl text-xs font-bold flex items-center space-x-2 transition ${
                        kudosGiven.includes(currentStory.id) ? 'bg-rose-600 text-white' : 'bg-rose-500/20 text-rose-300 border border-rose-500/40'
                      }`}
                    >
                      <HeartIcon className="w-4 h-4" fill={kudosGiven.includes(currentStory.id)} />
                      <span>{kudosGiven.includes(currentStory.id) ? 'Kudos Enviado' : 'Dejar Kudos'} ({currentStory.kudos})</span>
                    </button>

                    <button
                      onClick={() => toggleBookmark(currentStory.id)}
                      className={`px-4 py-2 rounded-xl text-xs font-bold flex items-center space-x-2 transition ${
                        bookmarks.includes(currentStory.id) ? 'bg-amber-500 text-slate-950' : 'bg-slate-800 text-slate-300'
                      }`}
                    >
                      <BookmarkIcon className="w-4 h-4" fill={bookmarks.includes(currentStory.id)} />
                      <span>{bookmarks.includes(currentStory.id) ? 'Guardado' : 'Guardar'}</span>
                    </button>

                    <button
                      onClick={() => {
                        setDonatingToAuthor(currentStory.author);
                        setDonationModalOpen(true);
                      }}
                      className="px-4 py-2 rounded-xl text-xs font-bold bg-emerald-600 hover:bg-emerald-500 text-white flex items-center space-x-1.5 shadow"
                    >
                      <GiftIcon className="w-4 h-4" />
                      <span>Donar al Autor</span>
                    </button>
                  </div>
                </div>
              </div>

              {/* Chapter Content Area */}
              {currentStory.chapters && currentStory.chapters[currentChapterIndex] && (
                <div className="py-8 space-y-6">
                  <h2 className="text-2xl font-bold text-center" style={{ color: currentStory.decorations?.accentColor || '#8b5cf6' }}>
                    {currentStory.chapters[currentChapterIndex].title}
                  </h2>

                  <div className="prose max-w-none text-base leading-relaxed whitespace-pre-line opacity-95">
                    {currentStory.chapters[currentChapterIndex].content}
                  </div>

                  {/* CHAPTER MEDIA ATTACHMENTS (Images and Videos) */}
                  {currentStory.chapters[currentChapterIndex].media && currentStory.chapters[currentChapterIndex].media.length > 0 && (
                    <div className="space-y-6 pt-6">
                      {currentStory.chapters[currentChapterIndex].media.map((item, mIdx) => (
                        <div key={mIdx} className="flex flex-col items-center justify-center my-4">
                          {item.type === 'image' && (
                            <img src={item.url} alt="Media adjunta" className="max-h-96 rounded-xl border border-slate-700 shadow-lg object-cover" />
                          )}
                          {item.type === 'video' && (
                            <video src={item.url} controls className="w-full max-w-2xl rounded-xl border border-slate-700 shadow-lg" />
                          )}
                          {item.type === 'youtube' && (
                            <div className="w-full max-w-2xl aspect-video rounded-xl overflow-hidden border border-slate-700 shadow-lg">
                              <iframe src={item.url} className="w-full h-full" allowFullScreen title="YouTube Video"></iframe>
                            </div>
                          )}
                          {item.caption && <p className="text-xs text-slate-400 mt-2 italic">{item.caption}</p>}
                        </div>
                      ))}
                    </div>
                  )}
                </div>
              )}

              {/* Chapter Selection Pagination */}
              {currentStory.chapters.length > 1 && (
                <div className="flex justify-between items-center border-t pt-4" style={{ borderColor: `${currentStory.decorations?.accentColor || '#8b5cf6'}40` }}>
                  <button
                    disabled={currentChapterIndex === 0}
                    onClick={() => setCurrentChapterIndex(prev => prev - 1)}
                    className="px-4 py-2 bg-slate-800 rounded-lg text-xs font-bold disabled:opacity-40"
                  >
                    Anterior
                  </button>
                  <span className="text-xs font-semibold">
                    Capítulo {currentChapterIndex + 1} de {currentStory.chapters.length}
                  </span>
                  <button
                    disabled={currentChapterIndex === currentStory.chapters.length - 1}
                    onClick={() => setCurrentChapterIndex(prev => prev + 1)}
                    className="px-4 py-2 bg-slate-800 rounded-lg text-xs font-bold disabled:opacity-40"
                  >
                    Siguiente
                  </button>
                </div>
              )}

            </div>
          </div>
        ) : (
          <>
            {/* VIEW: EXPLORE & SEARCH */}
            {activeTab === 'explore' && (
              <div className="space-y-6">
                
                {/* SEARCH & DYNAMIC TAG BAR */}
                <div className="bg-slate-900 border border-purple-900/50 p-4 rounded-2xl shadow-xl space-y-4">
                  <div className="flex flex-col sm:flex-row gap-3">
                    {/* Input search by name */}
                    <div className="relative flex-1">
                      <SearchIcon className="w-5 h-5 absolute left-3 top-3 text-slate-400" />
                      <input
                        type="text"
                        placeholder="Buscar historias por título o autor..."
                        value={searchQuery}
                        onChange={(e) => setSearchQuery(e.target.value)}
                        className="w-full bg-slate-950 border border-slate-800 rounded-xl pl-10 pr-4 py-2.5 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:border-purple-500"
                      />
                    </div>

                    {/* Fandom Filter Dropdown */}
                    <select
                      value={selectedFandom}
                      onChange={(e) => setSelectedFandom(e.target.value)}
                      className="bg-slate-950 border border-slate-800 rounded-xl px-4 py-2.5 text-sm text-slate-200 focus:outline-none focus:border-purple-500"
                    >
                      <option value="">Todos los Fandoms</option>
                      {fandomOptions.map((f, idx) => (
                        <option key={idx} value={f}>{f}</option>
                      ))}
                    </select>
                  </div>

                  {/* Tag List Chips */}
                  <div className="space-y-2">
                    <p className="text-xs font-bold text-slate-400 uppercase tracking-wider">Etiquetas populares:</p>
                    <div className="flex flex-wrap gap-1.5">
                      <button
                        onClick={() => setSelectedTag('')}
                        className={`px-3 py-1 rounded-full text-xs font-medium transition ${
                          selectedTag === '' ? 'bg-purple-600 text-white' : 'bg-slate-800 text-slate-400 hover:text-white'
                        }`}
                      >
                        Todas
                      </button>
                      {globalTags.map((tag, idx) => (
                        <button
                          key={idx}
                          onClick={() => setSelectedTag(tag === selectedTag ? '' : tag)}
                          className={`px-3 py-1 rounded-full text-xs font-medium transition ${
                            selectedTag === tag ? 'bg-amber-500 text-slate-950 font-bold' : 'bg-slate-800 text-slate-300 hover:bg-slate-700'
                          }`}
                        >
                          #{tag}
                        </button>
                      ))}
                    </div>
                  </div>
                </div>

                {/* STORIES GRID */}
                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  {filteredStories.map(story => (
                    <div 
                      key={story.id} 
                      className="bg-slate-900 border border-slate-800 rounded-2xl p-4 flex gap-4 hover:border-purple-500/50 transition duration-300 shadow-lg group relative overflow-hidden"
                    >
                      <img 
                        src={story.coverImage} 
                        alt={story.title} 
                        className="w-28 h-40 object-cover rounded-xl shadow-md border border-slate-800 flex-shrink-0 group-hover:scale-105 transition duration-300"
                      />
                      <div className="flex-1 flex flex-col justify-between">
                        <div className="space-y-1.5">
                          <span className="text-[10px] font-bold px-2 py-0.5 rounded bg-purple-950 text-purple-300 border border-purple-800/50">
                            {story.fandom}
                          </span>
                          <h3 
                            onClick={() => { setCurrentStory(story); setCurrentChapterIndex(0); }}
                            className="text-lg font-bold text-white hover:text-amber-400 cursor-pointer transition line-clamp-1"
                          >
                            {story.title}
                          </h3>
                          <p className="text-xs text-slate-400">Por <span className="text-slate-300 font-semibold">{story.author}</span></p>
                          <p className="text-xs text-slate-300 line-clamp-2 leading-relaxed pt-1">{story.synopsis}</p>
                        </div>

                        <div className="pt-3 flex items-center justify-between border-t border-slate-800/80">
                          <div className="flex items-center space-x-3 text-xs text-slate-400">
                            <span className="flex items-center space-x-1 text-rose-400">
                              <HeartIcon className="w-3.5 h-3.5" fill={true} />
                              <span>{story.kudos}</span>
                            </span>
                          </div>

                          <div className="flex items-center space-x-2">
                            <button
                              onClick={() => toggleBookmark(story.id)}
                              className={`p-1.5 rounded-lg transition ${
                                bookmarks.includes(story.id) ? 'text-amber-400 bg-amber-400/10' : 'text-slate-500 hover:text-slate-300'
                              }`}
                            >
                              <BookmarkIcon className="w-4 h-4" fill={bookmarks.includes(story.id)} />
                            </button>
                            <button
                              onClick={() => { setCurrentStory(story); setCurrentChapterIndex(0); }}
                              className="px-3 py-1.5 rounded-lg bg-purple-600 hover:bg-purple-500 text-white text-xs font-bold transition"
                            >
                              Leer
                            </button>
                          </div>
                        </div>

                      </div>
                    </div>
                  ))}
                </div>

              </div>
            )}

            {/* VIEW: PERSONAL LIBRARY */}
            {activeTab === 'library' && (
              <div className="space-y-6 max-w-5xl mx-auto">
                <div className="border-b border-purple-900/60 pb-4 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                  <div>
                    <h1 className="text-2xl font-black text-white flex items-center space-x-2">
                      <BookmarkIcon className="w-6 h-6 text-amber-300" fill={true} />
                      <span>Mi Biblioteca Personal</span>
                    </h1>
                    <p className="text-xs text-slate-400 mt-1">Historias guardadas para leer más tarde</p>
                  </div>
                </div>

                {bookmarks.length === 0 ? (
                  <div className="text-center py-16 bg-slate-900/50 rounded-2xl border border-dashed border-slate-800">
                    <p className="text-slate-400 text-sm">No tienes historias guardadas en tu biblioteca.</p>
                  </div>
                ) : (
                  <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                    {stories.filter(s => bookmarks.includes(s.id)).map(story => (
                      <div key={story.id} className="bg-slate-900 border border-slate-800 rounded-2xl p-4 flex gap-4">
                        <img src={story.coverImage} alt={story.title} className="w-24 h-36 object-cover rounded-xl" />
                        <div className="flex-1 flex flex-col justify-between">
                          <div>
                            <h3 className="font-bold text-base text-white">{story.title}</h3>
                            <p className="text-xs text-slate-400">Por {story.author}</p>
                          </div>
                          <button
                            onClick={() => { setCurrentStory(story); setCurrentChapterIndex(0); }}
                            className="px-3 py-1.5 bg-purple-600 rounded-lg text-xs font-bold text-white w-fit"
                          >
                            Continuar Lectura
                          </button>
                        </div>
                      </div>
                    ))}
                  </div>
                )}
              </div>
            )}

            {/* VIEW: WRITE & DECORATE STORY */}
            {activeTab === 'write' && (
              <div className="max-w-4xl mx-auto bg-slate-900 border border-purple-900/50 rounded-2xl p-6 sm:p-8 shadow-2xl space-y-6">
                <div>
                  <h1 className="text-2xl font-black text-white">Estudio de Creación de Historias</h1>
                  <p className="text-xs text-slate-400 mt-1">Escribe tu obra y personalízala visualmente con imágenes, videos y estilos de fondo.</p>
                </div>

                <form onSubmit={handlePublishStory} className="space-y-6">
                  {/* Story Metadata */}
                  <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                      <label className="block text-xs font-bold text-slate-300 uppercase mb-1">Título de la Historia *</label>
                      <input
                        type="text"
                        required
                        value={editorStory.title}
                        onChange={e => setEditorStory({ ...editorStory, title: e.target.value })}
                        className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2 text-sm text-white focus:outline-none focus:border-purple-500"
                      />
                    </div>

                    <div>
                      <label className="block text-xs font-bold text-slate-300 uppercase mb-1">Fandom / Categoria</label>
                      <input
                        type="text"
                        placeholder="Ej. Marvel, Genshin Impact, Original"
                        value={editorStory.fandom}
                        onChange={e => setEditorStory({ ...editorStory, fandom: e.target.value })}
                        className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2 text-sm text-white focus:outline-none focus:border-purple-500"
                      />
                    </div>
                  </div>

                  <div>
                    <label className="block text-xs font-bold text-slate-300 uppercase mb-1">Sinopsis *</label>
                    <textarea
                      required
                      rows={3}
                      value={editorStory.synopsis}
                      onChange={e => setEditorStory({ ...editorStory, synopsis: e.target.value })}
                      className="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-purple-500"
                    />
                  </div>

                  {/* Cover Export File Selection */}
                  <div className="border border-dashed border-slate-700 rounded-xl p-4 text-center bg-slate-950/50">
                    <label className="block text-xs font-bold text-slate-300 uppercase mb-2">Exportar Imagen de Portada (Obligatorio desde archivo local) *</label>
                    <input
                      type="file"
                      accept="image/*"
                      ref={editorFileInputRef}
                      onChange={handleCoverUpload}
                      className="hidden"
                    />
                    <button
                      type="button"
                      onClick={() => editorFileInputRef.current.click()}
                      className="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-bold rounded-lg"
                    >
                      Seleccionar Portada Local
                    </button>
                    {editorStory.coverImage && (
                      <div className="mt-3 flex justify-center">
                        <img src={editorStory.coverImage} alt="Portada exportada" className="h-32 w-24 object-cover rounded-md border border-purple-500" />
                      </div>
                    )}
                  </div>

                  {/* Tags and Relationships */}
                  <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                      <label className="block text-xs font-bold text-slate-300 uppercase mb-1">Relaciones / Ships (separadas por coma)</label>
                      <input
                        type="text"
                        placeholder="Ej. Slow Burn, Enemies to Lovers"
                        value={editorStory.relationships}
                        onChange={e => setEditorStory({ ...editorStory, relationships: e.target.value })}
                        className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2 text-sm text-white"
                      />
                    </div>
                    <div>
                      <label className="block text-xs font-bold text-slate-300 uppercase mb-1">Etiquetas / Tags (separadas por coma)</label>
                      <input
                        type="text"
                        placeholder="Ej. Fantasía, Romance, AU"
                        value={editorStory.tags}
                        onChange={e => setEditorStory({ ...editorStory, tags: e.target.value })}
                        className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2 text-sm text-white"
                      />
                    </div>
                  </div>

                  {/* CUSTOM STORY DECORATIONS */}
                  <div className="p-4 bg-slate-950 rounded-xl border border-purple-900/40 space-y-3">
                    <h3 className="text-xs font-bold text-amber-400 uppercase tracking-wider">Decoración del Libro (Estilos de Lectura)</h3>
                    <div className="grid grid-cols-2 sm:grid-cols-4 gap-4">
                      <div>
                        <label className="block text-[10px] text-slate-400 mb-1">Color Fondo</label>
                        <input
                          type="color"
                          value={editorStory.bgColor}
                          onChange={e => setEditorStory({ ...editorStory, bgColor: e.target.value })}
                          className="w-full h-8 rounded bg-transparent cursor-pointer"
                        />
                      </div>
                      <div>
                        <label className="block text-[10px] text-slate-400 mb-1">Color Texto</label>
                        <input
                          type="color"
                          value={editorStory.textColor}
                          onChange={e => setEditorStory({ ...editorStory, textColor: e.target.value })}
                          className="w-full h-8 rounded bg-transparent cursor-pointer"
                        />
                      </div>
                      <div>
                        <label className="block text-[10px] text-slate-400 mb-1">Color Acento</label>
                        <input
                          type="color"
                          value={editorStory.accentColor}
                          onChange={e => setEditorStory({ ...editorStory, accentColor: e.target.value })}
                          className="w-full h-8 rounded bg-transparent cursor-pointer"
                        />
                      </div>
                      <div>
                        <label className="block text-[10px] text-slate-400 mb-1">Tipografía</label>
                        <select
                          value={editorStory.fontFamily}
                          onChange={e => setEditorStory({ ...editorStory, fontFamily: e.target.value })}
                          className="w-full bg-slate-900 border border-slate-800 text-xs text-white p-1.5 rounded"
                        >
                          <option value="sans-serif">Sans Serif</option>
                          <option value="serif">Serif (Clásico)</option>
                          <option value="monospace">Monospace</option>
                        </select>
                      </div>
                    </div>
                  </div>

                  {/* CHAPTER CONTENT & MEDIA ATTACHMENTS */}
                  <div className="space-y-4">
                    <h3 className="text-sm font-bold text-white">Contenido del Capítulo</h3>
                    <input
                      type="text"
                      placeholder="Título del Capítulo"
                      value={editorStory.chapters[activeEditorChapter]?.title || ''}
                      onChange={e => {
                        const updated = [...editorStory.chapters];
                        updated[activeEditorChapter].title = e.target.value;
                        setEditorStory({ ...editorStory, chapters: updated });
                      }}
                      className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-2 text-sm text-white"
                    />

                    <textarea
                      rows={8}
                      placeholder="Escribe tu historia aquí... (Puedes pegar imágenes directamente con Ctrl+V o usar los botones de abajo)"
                      value={editorStory.chapters[activeEditorChapter]?.content || ''}
                      onPaste={handlePasteImage}
                      onChange={e => {
                        const updated = [...editorStory.chapters];
                        updated[activeEditorChapter].content = e.target.value;
                        setEditorStory({ ...editorStory, chapters: updated });
                      }}
                      className="w-full bg-slate-950 border border-slate-800 rounded-xl p-4 text-sm text-white focus:outline-none focus:border-purple-500"
                    />

                    {/* MEDIA ATTACHMENT CONTROLS */}
                    <div className="p-4 bg-slate-950 rounded-xl border border-slate-800 space-y-3">
                      <p className="text-xs font-bold text-slate-300">Adjuntar Multimedia al Capítulo:</p>

                      <div className="flex flex-wrap gap-3">
                        {/* Image file export */}
                        <input
                          type="file"
                          accept="image/*"
                          multiple
                          ref={chapterMediaInputRef}
                          onChange={handleChapterImageUpload}
                          className="hidden"
                        />
                        <button
                          type="button"
                          onClick={() => chapterMediaInputRef.current.click()}
                          className="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 rounded-lg text-xs font-semibold text-slate-200 flex items-center space-x-1.5"
                        >
                          <ImageIcon className="w-4 h-4 text-purple-400" />
                          <span>Exportar Imagen</span>
                        </button>

                        {/* Video file export */}
                        <input
                          type="file"
                          accept="video/*"
                          ref={videoInputRef}
                          onChange={handleVideoUpload}
                          className="hidden"
                        />
                        <button
                          type="button"
                          onClick={() => videoInputRef.current.click()}
                          className="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 rounded-lg text-xs font-semibold text-slate-200 flex items-center space-x-1.5"
                        >
                          <VideoIcon className="w-4 h-4 text-pink-400" />
                          <span>Exportar Video Local</span>
                        </button>
                      </div>

                      {/* YouTube Link Embed Input */}
                      <div className="flex gap-2 pt-2">
                        <input
                          type="text"
                          placeholder="Pegar enlace de YouTube (ej. https://www.youtube.com/watch?v=...)"
                          value={youtubeUrlInput}
                          onChange={e => setYoutubeUrlInput(e.target.value)}
                          className="flex-1 bg-slate-900 border border-slate-800 rounded-lg px-3 py-1.5 text-xs text-white"
                        />
                        <button
                          type="button"
                          onClick={handleAddYoutubeVideo}
                          className="px-3 py-1.5 bg-red-600 hover:bg-red-500 text-white rounded-lg text-xs font-bold"
                        >
                          Agregar YouTube
                        </button>
                      </div>

                      {/* Preview Attached Media */}
                      {editorStory.chapters[activeEditorChapter]?.media.length > 0 && (
                        <div className="pt-2 flex flex-wrap gap-2">
                          {editorStory.chapters[activeEditorChapter].media.map((m, idx) => (
                            <div key={idx} className="relative group text-xs bg-slate-900 p-2 rounded border border-slate-800 flex items-center space-x-2">
                              <span>{m.type === 'image' ? '🖼️ Imagen' : '🎥 Video'}</span>
                              <button
                                type="button"
                                onClick={() => {
                                  const updated = [...editorStory.chapters];
                                  updated[activeEditorChapter].media.splice(idx, 1);
                                  setEditorStory({ ...editorStory, chapters: updated });
                                }}
                                className="text-red-400 font-bold ml-2"
                              >
                                ✕
                              </button>
                            </div>
                          ))}
                        </div>
                      )}
                    </div>
                  </div>

                  <button
                    type="submit"
                    className="w-full py-3 bg-gradient-to-r from-purple-600 to-amber-500 hover:from-purple-500 hover:to-amber-400 text-slate-950 font-black rounded-xl text-sm shadow-xl uppercase tracking-wider"
                  >
                    Publicar Historia en Comunity Fan
                  </button>
                </form>
              </div>
            )}
          </>
        )}

      </main>

      {/* DONATION MODAL */}
      {donationModalOpen && (
        <div className="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4">
          <div className="bg-slate-900 border border-emerald-500/40 rounded-2xl p-6 max-w-md w-full space-y-4">
            <h2 className="text-xl font-bold text-white flex items-center space-x-2">
              <GiftIcon className="w-5 h-5 text-emerald-400" />
              <span>Donar a {donatingToAuthor}</span>
            </h2>
            <p className="text-xs text-slate-400">Apoya directamente a este autor para que siga creando historias increíbles.</p>

            <div className="space-y-3">
              <div>
                <label className="block text-xs font-semibold text-slate-300 mb-1">Monto de la donación ($USD)</label>
                <div className="flex gap-2">
                  {['2.00', '5.00', '10.00', '20.00'].map(val => (
                    <button
                      key={val}
                      onClick={() => setDonationAmount(val)}
                      className={`flex-1 py-1.5 rounded-lg text-xs font-bold ${
                        donationAmount === val ? 'bg-emerald-500 text-slate-950' : 'bg-slate-800 text-slate-300'
                      }`}
                    >
                      ${val}
                    </button>
                  ))}
                </div>
              </div>

              <div>
                <label className="block text-xs font-semibold text-slate-300 mb-1">Mensaje para el autor (Opcional)</label>
                <textarea
                  rows={2}
                  value={donationMessage}
                  onChange={e => setDonationMessage(e.target.value)}
                  placeholder="¡Me encantó tu historia!"
                  className="w-full bg-slate-950 border border-slate-800 rounded-xl p-2.5 text-xs text-white"
                />
              </div>
            </div>

            <div className="flex justify-end space-x-2 pt-2">
              <button
                onClick={() => setDonationModalOpen(false)}
                className="px-4 py-2 bg-slate-800 text-xs font-bold text-slate-300 rounded-lg"
              >
                Cancelar
              </button>
              <button
                onClick={() => {
                  alert(`¡Gracias por tu donación de $${donationAmount} a ${donatingToAuthor}!`);
                  setDonationModalOpen(false);
                }}
                className="px-4 py-2 bg-emerald-600 hover:bg-emerald-500 text-xs font-bold text-white rounded-lg shadow"
              >
                Confirmar Donación
              </button>
            </div>
          </div>
        </div>
      )}

      {/* AUTH MODAL */}
      {authModalOpen && (
        <div className="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4">
          <div className="bg-slate-900 border border-purple-900/60 rounded-2xl p-6 max-w-sm w-full space-y-4">
            <h2 className="text-xl font-extrabold text-white">
              {isRegistering ? 'Crear Cuenta' : 'Iniciar Sesión'}
            </h2>

            <form onSubmit={handleAuthSubmit} className="space-y-3">
              {isRegistering && (
                <div>
                  <label className="block text-xs text-slate-400 mb-1">Nombre de Usuario</label>
                  <input
                    type="text"
                    required
                    value={authUsername}
                    onChange={e => setAuthUsername(e.target.value)}
                    className="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-sm text-white"
                  />
                </div>
              )}
              <div>
                <label className="block text-xs text-slate-400 mb-1">Correo Electrónico</label>
                <input
                  type="email"
                  required
                  value={authEmail}
                  onChange={e => setAuthEmail(e.target.value)}
                  className="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-sm text-white"
                />
              </div>
              <div>
                <label className="block text-xs text-slate-400 mb-1">Contraseña</label>
                <input
                  type="password"
                  required
                  value={authPassword}
                  onChange={e => setAuthPassword(e.target.value)}
                  className="w-full bg-slate-950 border border-slate-800 rounded-lg p-2 text-sm text-white"
                />
              </div>

              <button
                type="submit"
                className="w-full py-2.5 bg-purple-600 hover:bg-purple-500 text-white font-bold text-sm rounded-lg shadow"
              >
                {isRegistering ? 'Registrarse' : 'Entrar'}
              </button>
            </form>

            <div className="text-center pt-2">
              <button
                onClick={() => setIsRegistering(!isRegistering)}
                className="text-xs text-purple-400 hover:underline"
              >
                {isRegistering ? '¿Ya tienes cuenta? Inicia sesión' : '¿No tienes cuenta? Regístrate'}
              </button>
            </div>
          </div>
        </div>
      )}

      {/* FOOTER */}
      <footer className="bg-slate-950 border-t border-slate-900 py-6 text-center text-xs text-slate-500">
        <p>© 2026 Comunity Fan - Comunidad de Lectores y Escritores Creativos.</p>
      </footer>
    </div>
  );
}
