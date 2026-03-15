import React, { useState, useEffect, useRef } from 'react';
import { 
  Camera, 
  Video, 
  Palette, 
  Instagram, 
  Twitter, 
  Mail, 
  ArrowRight, 
  ArrowLeft,
  ExternalLink,
  ChevronDown,
  Menu,
  X,
  Github,
  Linkedin,
  Sparkles
} from 'lucide-react';

// --- Parallax Scroll Hook ---
const useParallax = (speed = 0.4) => {
  const [offset, setOffset] = useState(0);
  
  useEffect(() => {
    let animationFrameId;
    const handleScroll = () => {
      animationFrameId = requestAnimationFrame(() => {
        setOffset(window.scrollY * speed);
      });
    };
    window.addEventListener('scroll', handleScroll, { passive: true });
    return () => {
      window.removeEventListener('scroll', handleScroll);
      if(animationFrameId) cancelAnimationFrame(animationFrameId);
    };
  }, [speed]);

  return offset;
};

// --- Background Texture & Effects ---
const BackgroundTexture = () => {
  return (
    <div className="fixed inset-0 pointer-events-none z-0 overflow-hidden">
      {/* Dot Matrix Pattern */}
      <div className="absolute inset-0 opacity-[0.05]" 
           style={{ backgroundImage: 'radial-gradient(#f97316 1.5px, transparent 1.5px)', backgroundSize: '32px 32px' }}>
      </div>
      
      {/* Animated Ambient Swirls / Glows */}
      <div className="absolute top-[-20%] left-[-10%] w-[70vw] h-[70vw] bg-orange-600/10 rounded-full blur-[120px] mix-blend-screen animate-[spin_20s_linear_infinite]"></div>
      <div className="absolute bottom-[-20%] right-[-10%] w-[60vw] h-[60vw] bg-amber-600/10 rounded-full blur-[100px] mix-blend-screen animate-[spin_25s_linear_infinite_reverse]"></div>
      
      {/* Gritty Noise Overlay */}
      <svg className="absolute w-0 h-0">
        <filter id="noiseFilter">
          <feTurbulence type="fractalNoise" baseFrequency="0.7" numOctaves="3" stitchTiles="stitch" />
        </filter>
      </svg>
      <div className="absolute inset-0 opacity-[0.03] mix-blend-overlay" style={{ filter: 'url(#noiseFilter)' }}></div>
    </div>
  );
};

// --- Flame Cursor Effect ---
const CursorGlow = () => {
  const cursorRef = useRef(null);
  const trailingRef = useRef(null);

  useEffect(() => {
    let mouseX = 0;
    let mouseY = 0;
    let trailingX = 0;
    let trailingY = 0;

    const onMouseMove = (e) => {
      mouseX = e.clientX;
      mouseY = e.clientY;
      
      if (cursorRef.current) {
        cursorRef.current.style.transform = `translate3d(${mouseX}px, ${mouseY}px, 0)`;
      }
    };

    const animateTrailing = () => {
      // Increased from 0.15 to 0.2 for a slightly tighter, less draggy trail
      trailingX += (mouseX - trailingX) * 0.2;
      trailingY += (mouseY - trailingY) * 0.2;
      
      if (trailingRef.current) {
        trailingRef.current.style.transform = `translate3d(${trailingX}px, ${trailingY}px, 0)`;
      }
      requestAnimationFrame(animateTrailing);
    };

    window.addEventListener('mousemove', onMouseMove);
    const animationId = requestAnimationFrame(animateTrailing);

    return () => {
      window.removeEventListener('mousemove', onMouseMove);
      cancelAnimationFrame(animationId);
    };
  }, []);

  return (
    <>
      <div 
        ref={cursorRef}
        className="pointer-events-none fixed top-0 left-0 w-1.5 h-1.5 -ml-[3px] -mt-[3px] bg-orange-200/80 rounded-full shadow-[0_0_10px_1px_rgba(249,115,22,0.5)] z-[100] transition-opacity duration-300 hidden md:block mix-blend-screen"
      />
      <div 
        ref={trailingRef}
        className="pointer-events-none fixed top-0 left-0 w-20 h-20 -ml-10 -mt-10 bg-gradient-to-r from-orange-500/20 to-amber-500/10 rounded-full blur-[20px] z-[99] hidden md:block mix-blend-screen"
      />
    </>
  );
};

// --- 2D Sketched Camera Component ---
const CameraSketch = () => {
  return (
    <div className="w-[120px] h-[120px] md:w-[180px] md:h-[180px] pointer-events-none float-animation flex items-center justify-center opacity-80 mt-8 md:mt-0 md:ml-8">
      <svg 
        viewBox="0 0 100 100" 
        className="w-full h-full text-white/60 drop-shadow-2xl"
        fill="none" 
        stroke="currentColor" 
        strokeWidth="1.5"
        strokeLinecap="round" 
        strokeLinejoin="round"
      >
        {/* Flash/Viewfinder Top */}
        <path className="sketch-path" d="M30 35 L38 22 L62 22 L70 35" />
        
        {/* Main Body */}
        <rect className="sketch-path" x="12" y="35" width="76" height="50" rx="8" />
        
        {/* Outer Lens */}
        <circle className="sketch-path delay-1" cx="50" cy="60" r="16" />
        
        {/* Inner Lens with Orange Accent */}
        <circle className="sketch-path delay-2" cx="50" cy="60" r="7" stroke="#f97316" strokeWidth="2" />
        
        {/* Shutter Button */}
        <rect className="sketch-path delay-3" x="20" y="28" width="10" height="7" rx="2" />
        
        {/* Decorative Dial */}
        <path className="sketch-path delay-3" d="M72 32 L82 32 M74 35 L80 35" strokeWidth="2" />
        
        {/* Sketchy crosshairs (Orange) */}
        <path className="sketch-path delay-2 text-orange-500" stroke="#f97316" strokeWidth="0.5" d="M50 35 L50 40 M50 80 L50 85 M25 60 L30 60 M70 60 L75 60" />
      </svg>
    </div>
  );
};

// --- Assets & Data ---
const PROFILE_IMAGE = "IMG_0895.jpg"; 

const PROJECTS = [
  // Photography
  { id: 1, title: "Urban Echoes", category: "Photography", image: "https://images.unsplash.com/photo-1514565131-fce0801e5785?auto=format&fit=crop&q=80&w=800", description: "A street photography series exploring neon-lit cityscapes." },
  { id: 2, title: "Architectural Lines", category: "Photography", image: "https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?auto=format&fit=crop&q=80&w=800", description: "Exploring symmetry in modern brutalist architecture." },
  { id: 3, title: "Desert Silence", category: "Photography", image: "https://images.unsplash.com/photo-1473448912268-2022ce9509d8?auto=format&fit=crop&q=80&w=800", description: "Landscape photography highlighting isolation." },
  { id: 4, title: "Neon Nights", category: "Photography", image: "https://images.unsplash.com/photo-1555617981-dd30510d9311?auto=format&fit=crop&q=80&w=800", description: "High-contrast portraits in downtown districts." },
  { id: 5, title: "Candid Moments", category: "Photography", image: "https://images.unsplash.com/photo-1511895426328-dc8714191300?auto=format&fit=crop&q=80&w=800", description: "Documentary-style event and street photography." },
  
  // Video
  { id: 6, title: "Cinematic Moods", category: "Video", image: "https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?auto=format&fit=crop&q=80&w=800", description: "Color grading and editing for a short narrative film." },
  { id: 7, title: "Music Video Montage", category: "Video", image: "https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&q=80&w=800", description: "High-energy editing for a local indie artist." },
  { id: 8, title: "Corporate Anthem", category: "Video", image: "https://images.unsplash.com/photo-1601506521937-0121a7fc2a6b?auto=format&fit=crop&q=80&w=800", description: "Brand storytelling for an upcoming tech firm." },
  { id: 9, title: "Short Film: Lost", category: "Video", image: "https://images.unsplash.com/photo-1485846234645-a62644f84728?auto=format&fit=crop&q=80&w=800", description: "Director of Photography for an award-winning short." },
  { id: 10, title: "Documentary Reel", category: "Video", image: "https://images.unsplash.com/photo-1574717024653-61fd2cf4d44d?auto=format&fit=crop&q=80&w=800", description: "Highlights from 2023 documentary commissions." },

  // Design
  { id: 11, title: "Brand Identity: VORTEX", category: "Design", image: "https://images.unsplash.com/photo-1634942537034-2531766767d1?auto=format&fit=crop&q=80&w=800", description: "Minimalist visual identity for a tech startup." },
  { id: 12, title: "Editorial Layout", category: "Design", image: "https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&q=80&w=800", description: "Print design for a contemporary fashion magazine." },
  { id: 13, title: "Web 3.0 UI", category: "Design", image: "https://images.unsplash.com/photo-1618761714954-0b8cd0026356?auto=format&fit=crop&q=80&w=800", description: "Dark-mode interface design for a crypto dashboard." },
  { id: 14, title: "Product Packaging", category: "Design", image: "https://images.unsplash.com/photo-1628102491629-77858ab5741f?auto=format&fit=crop&q=80&w=800", description: "Minimalist sustainable packaging for skincare." },
  { id: 15, title: "Logo Collection", category: "Design", image: "https://images.unsplash.com/photo-1626785774573-4b799315345d?auto=format&fit=crop&q=80&w=800", description: "A curation of my favorite logomarks from 2021-2024." }
];

const SKILLS = [
  { name: "Art Direction", icon: <Palette size={20} />, level: "Expert" },
  { name: "Cinematography", icon: <Video size={20} />, level: "Advanced" },
  { name: "Post-Processing", icon: <Camera size={20} />, level: "Expert" },
  { name: "Motion Graphics", icon: <Video size={20} />, level: "Intermediate" }
];

const Navbar = () => {
  const [scrolled, setScrolled] = useState(false);
  const [isOpen, setIsOpen] = useState(false);

  useEffect(() => {
    const handleScroll = () => setScrolled(window.scrollY > 50);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const navLinks = [
    { name: 'About', href: '#about' },
    { name: 'Photography', href: '#photography' },
    { name: 'Video', href: '#video' },
    { name: 'Design', href: '#design' },
  ];

  return (
    <nav className={`fixed top-0 w-full z-50 transition-all duration-500 ${scrolled ? 'bg-black/80 backdrop-blur-xl py-4 border-b border-white/5' : 'bg-transparent py-8'}`}>
      <div className="max-w-7xl mx-auto px-6 flex justify-between items-center">
        <a href="#" className="text-xl font-black tracking-[0.25em] text-white">
          AMINE<span className="text-orange-500">.</span>
        </a>
        <div className="hidden md:flex items-center space-x-10">
          {navLinks.map((link) => (
            <a key={link.name} href={link.href} className="text-[10px] uppercase tracking-[0.3em] font-medium text-gray-400 hover:text-white transition-all">
              {link.name}
            </a>
          ))}
          <a href="#contact" className="px-6 py-2 bg-white/5 border border-white/10 rounded-full text-[10px] uppercase tracking-[0.3em] font-bold text-white hover:bg-orange-500 hover:text-white transition-all">
            Hire Me
          </a>
        </div>
        <button className="md:hidden text-white" onClick={() => setIsOpen(!isOpen)}>
          {isOpen ? <X /> : <Menu />}
        </button>
      </div>
      {isOpen && (
        <div className="md:hidden absolute top-full left-0 w-full bg-black border-b border-white/10 p-10 flex flex-col space-y-6 animate-in fade-in slide-in-from-top-4">
          {navLinks.map((link) => (
            <a key={link.name} href={link.href} className="text-2xl font-bold text-white uppercase tracking-tighter" onClick={() => setIsOpen(false)}>
              {link.name}
            </a>
          ))}
        </div>
      )}
    </nav>
  );
};

const Hero = () => {
  // Apply smooth parallax offset mapped to scroll position
  const parallaxOffsetY = useParallax(0.4);

  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden bg-transparent text-white px-6">
      <div className="absolute inset-0 w-full h-full pointer-events-none overflow-hidden">
        <img 
          src={PROFILE_IMAGE} 
          alt="Amine Ahenjir"
          style={{ transform: `translate3d(0, ${parallaxOffsetY}px, 0) scale(1.15)` }} // Scale prevents gaps during translation
          className="absolute inset-0 w-full h-full object-cover object-[70%_center] lg:object-right grayscale opacity-40 mix-blend-luminosity will-change-transform"
          onError={(e) => { e.target.src = "https://images.unsplash.com/photo-1594909122845-11baa439b7bf?q=80&w=2070&auto=format&fit=crop"; }}
        />
        {/* Dark gradient sweeping from the left to keep text crisp and readable */}
        <div className="absolute inset-0 bg-gradient-to-r from-black via-black/80 to-transparent z-10"></div>
        {/* Top and bottom vignette for a cinematic fade */}
        <div className="absolute inset-0 bg-gradient-to-b from-black/80 via-transparent to-black/80 z-10"></div>
      </div>

      <div className="relative z-20 w-full max-w-7xl mx-auto flex flex-col items-start">
        <div className="inline-flex items-center gap-2 px-4 py-1.5 mb-8 border border-white/10 rounded-full bg-white/5 backdrop-blur-sm animate-in fade-in slide-in-from-bottom-4 duration-700">
          <Sparkles size={12} className="text-orange-400" />
          <span className="text-[9px] font-bold tracking-[0.4em] uppercase text-gray-300">Designer & Cinematographer</span>
        </div>
        
        <div className="flex flex-col md:flex-row md:items-center gap-4 mb-6">
          <h1 className="text-7xl md:text-[10rem] font-black tracking-tighter leading-[0.82] animate-in fade-in slide-in-from-bottom-8 duration-1000 uppercase">
            Amine <br /> 
            <span className="text-transparent bg-clip-text bg-gradient-to-r from-orange-400 via-amber-300 to-orange-600">
              Ahenjir.
            </span>
          </h1>
          <div className="animate-in fade-in slide-in-from-right duration-1000 delay-300">
            <CameraSketch />
          </div>
        </div>
        
        <p className="text-xl md:text-2xl text-gray-400 mb-12 max-w-xl font-thin leading-relaxed animate-in fade-in slide-in-from-bottom-12 duration-1000">
          Capturing stories through a pixel-perfect lens. Expert in high-end videography and brand-first design.
        </p>
        
        <div className="flex flex-col sm:flex-row items-center gap-8 animate-in fade-in slide-in-from-bottom-16 duration-1000">
          <a href="#photography" className="group relative px-12 py-5 bg-white text-black font-black uppercase text-xs tracking-widest rounded-full overflow-hidden transition-all duration-300">
            <span className="relative z-10 flex items-center gap-2">Explore Portfolio <ArrowRight size={16} /></span>
            <div className="absolute inset-0 bg-orange-600 -translate-x-full group-hover:translate-x-0 transition-transform duration-300"></div>
            <style dangerouslySetInnerHTML={{ __html: `.group:hover span { color: white; }` }} />
          </a>
          <a href="#contact" className="text-[10px] font-bold uppercase tracking-[0.4em] text-gray-400 hover:text-white transition-colors border-b border-transparent hover:border-white pb-1">
            Get in touch
          </a>
        </div>
      </div>
    </section>
  );
};

const AboutSection = () => {
  const parallaxOffsetY = useParallax(0.25); // Slower parallax for the about image

  return (
    <section id="about" className="py-32 bg-zinc-950/40 backdrop-blur-md relative z-10 px-6">
      <div className="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-24 items-center">
        <div className="relative">
          <div className="rounded-3xl overflow-hidden border border-white/10 group grayscale hover:grayscale-0 transition-all duration-1000 relative">
             <img 
               src={PROFILE_IMAGE} 
               alt="Amine Ahenjir" 
               style={{ transform: `translate3d(0, ${parallaxOffsetY - 100}px, 0) scale(1.2)` }}
               className="w-full h-[600px] object-cover will-change-transform" 
               onError={(e) => { e.target.src = "https://images.unsplash.com/photo-1594909122845-11baa439b7bf?q=80&w=2070&auto=format&fit=crop"; }}
             />
             <div className="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent"></div>
          </div>
        </div>
        <div>
          <h3 className="text-orange-500 text-[10px] font-bold uppercase tracking-[0.5em] mb-6">Manifesto</h3>
          <h2 className="text-5xl md:text-7xl font-black text-white mb-8 tracking-tighter uppercase">Amine Ahenjir</h2>
          <div className="space-y-8 text-gray-400 text-xl font-thin leading-relaxed">
            <p>My work exists at the intersection of mathematical precision and cinematic emotion. I believe that every design should have a rhythm, and every video should have a soul.</p>
            <p>With a background in both technical design and visual arts, I bridge the gap between "how it looks" and "how it feels."</p>
            <div className="grid grid-cols-2 gap-8 pt-6">
              <div>
                <span className="block text-white text-4xl font-black">150+</span>
                <span className="text-[9px] uppercase tracking-[0.3em] text-gray-600 font-bold">Projects</span>
              </div>
              <div>
                <span className="block text-white text-4xl font-black">2024</span>
                <span className="text-[9px] uppercase tracking-[0.3em] text-gray-600 font-bold">Open for Bookings</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  );
};

// --- Reusable Horizontal Scrolling Category Carousel ---
const CategoryCarousel = ({ id, title, subtitle, items }) => {
  const scrollRef = useRef(null);

  const scroll = (direction) => {
    const { current } = scrollRef;
    if (current) {
      // Scrolls by about 80% of the visible container width
      const scrollAmount = current.clientWidth * 0.8;
      current.scrollBy({ 
        left: direction === 'left' ? -scrollAmount : scrollAmount, 
        behavior: 'smooth' 
      });
    }
  };

  return (
    <section id={id} className="py-24 bg-transparent relative z-10 px-6 overflow-hidden">
      {/* Header */}
      <div className="max-w-7xl mx-auto mb-12 flex flex-col justify-start">
        <h2 className="text-6xl md:text-[8rem] font-black text-white tracking-tighter leading-none uppercase opacity-20 transition-opacity duration-700 hover:opacity-100">{title}</h2>
        <p className="text-orange-500 text-[10px] font-bold uppercase tracking-[0.5em] mt-4 md:ml-2">{subtitle}</p>
      </div>

      {/* Scrolling Carousel */}
      <div 
        ref={scrollRef} 
        className="flex gap-8 overflow-x-auto snap-x snap-mandatory hide-scrollbar pb-8 max-w-7xl mx-auto"
      >
        {items.map((project, idx) => (
          <div 
            key={project.id} 
            className="min-w-[85vw] md:min-w-[45vw] lg:min-w-[32vw] snap-center group relative aspect-[4/5] rounded-3xl overflow-hidden cursor-pointer bg-zinc-900 border border-white/5 animate-in fade-in"
            style={{ animationDelay: `${idx * 100}ms` }}
          >
            <img 
              src={project.image} 
              alt={project.title} 
              className="w-full h-full object-cover grayscale group-hover:grayscale-0 transition-all duration-1000 group-hover:scale-110 opacity-70 group-hover:opacity-100" 
            />
            <div className="absolute inset-0 bg-gradient-to-t from-black/95 via-black/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 p-8 flex flex-col justify-end">
              <span className="text-orange-500 text-[9px] font-bold uppercase tracking-[0.4em] mb-3 flex items-center gap-2">
                <ExternalLink size={12} /> View Details
              </span>
              <h3 className="text-3xl font-black text-white uppercase tracking-tight leading-none mb-3">{project.title}</h3>
              <p className="text-gray-400 font-thin text-sm leading-relaxed">{project.description}</p>
            </div>
          </div>
        ))}
      </div>

      {/* Footer Navigation & Explore More */}
      <div className="max-w-7xl mx-auto mt-8 flex flex-col sm:flex-row items-center justify-between gap-8 border-t border-white/10 pt-8">
        <a href={`#${id}-all`} className="group flex items-center gap-4 text-[10px] font-bold uppercase tracking-[0.4em] text-white hover:text-orange-400 transition-colors">
          <span className="relative overflow-hidden pb-1">
            Explore All {title}
            <span className="absolute bottom-0 left-0 w-full h-[1px] bg-orange-400 -translate-x-full group-hover:translate-x-0 transition-transform duration-300"></span>
          </span>
          <ArrowRight size={14} className="group-hover:translate-x-2 transition-transform duration-300" />
        </a>

        <div className="flex gap-4">
          <button 
            onClick={() => scroll('left')} 
            className="p-4 rounded-full border border-white/20 text-white hover:text-orange-400 hover:border-orange-400 hover:bg-orange-500/10 hover:shadow-[0_0_20px_rgba(249,115,22,0.2)] hover:scale-110 transition-all duration-500 active:scale-95 outline-none focus:ring-2 focus:ring-orange-500/50"
            aria-label="Scroll left"
          >
            <ArrowLeft size={18} />
          </button>
          <button 
            onClick={() => scroll('right')} 
            className="p-4 rounded-full border border-white/20 text-white hover:text-orange-400 hover:border-orange-400 hover:bg-orange-500/10 hover:shadow-[0_0_20px_rgba(249,115,22,0.2)] hover:scale-110 transition-all duration-500 active:scale-95 outline-none focus:ring-2 focus:ring-orange-500/50"
            aria-label="Scroll right"
          >
            <ArrowRight size={18} />
          </button>
        </div>
      </div>
    </section>
  );
};

const SkillsSection = () => {
  return (
    <section id="services" className="py-32 bg-zinc-950/40 backdrop-blur-md relative z-10 px-6 border-y border-white/5 mt-12">
      <div className="max-w-7xl mx-auto flex flex-col items-center text-center">
        <h2 className="text-5xl md:text-[6rem] font-black text-white mb-16 tracking-tighter uppercase">Toolkit</h2>
        <div className="grid grid-cols-1 md:grid-cols-4 gap-8 w-full">
          {SKILLS.map((skill, idx) => (
            <div key={idx} className="p-10 border border-white/5 rounded-[2rem] bg-black hover:border-orange-500/50 transition-all group">
              <div className="flex justify-center text-gray-400 group-hover:text-orange-500 mb-8 transition-colors">
                {React.cloneElement(skill.icon, { size: 40 })}
              </div>
              <h4 className="text-white text-lg font-black uppercase tracking-widest mb-2">{skill.name}</h4>
              <div className="h-[2px] w-8 bg-orange-500 mx-auto opacity-0 group-hover:opacity-100 transition-opacity"></div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
};

const ContactSection = () => {
  return (
    <section id="contact" className="py-32 bg-transparent relative z-10 px-6">
      <div className="max-w-5xl mx-auto text-center">
        <h2 className="text-5xl md:text-8xl font-black text-white mb-12 tracking-tighter leading-none uppercase">Build <br /><span className="opacity-20">Legacy.</span></h2>
        <a href="mailto:amineahenjir@gmail.com" className="text-2xl md:text-5xl font-thin text-white hover:text-orange-400 transition-all tracking-tighter">amineahenjir@gmail.com</a>
        <div className="mt-24 flex justify-center gap-10">
          {[
            { Icon: Instagram, url: "https://www.instagram.com/amine.ahenjir/" },
            { Icon: Linkedin, url: "https://www.linkedin.com/in/amine-ahenjir-477a11255/" }
          ].map(({ Icon, url }, i) => (
            <a key={i} href={url} target="_blank" rel="noopener noreferrer" className="text-gray-600 hover:text-white transition-all transform hover:scale-125"><Icon size={24} /></a>
          ))}
        </div>
      </div>
    </section>
  );
};

const Footer = () => {
  return (
    <footer className="py-12 bg-black/40 backdrop-blur-md relative z-10 border-t border-white/5 px-6 text-center">
      <p className="text-[9px] text-gray-700 uppercase tracking-[0.8em] font-bold">Amine Ahenjir © {new Date().getFullYear()} — Futura 100 Edition</p>
    </footer>
  );
};

export default function App() {
  const photoProjects = PROJECTS.filter(p => p.category === 'Photography');
  const videoProjects = PROJECTS.filter(p => p.category === 'Video');
  const designProjects = PROJECTS.filter(p => p.category === 'Design');

  return (
    <div className="bg-black min-h-screen selection:bg-orange-600 selection:text-white antialiased">
      <BackgroundTexture />
      <CursorGlow />
      <Navbar />
      <main>
        <Hero />
        <AboutSection />
        
        {/* The new segregated Carousel sections */}
        <div className="flex flex-col gap-12">
          <CategoryCarousel id="photography" title="Photography" subtitle="Capturing the moment" items={photoProjects} />
          <CategoryCarousel id="video" title="Videography" subtitle="Motion & Storytelling" items={videoProjects} />
          <CategoryCarousel id="design" title="Design" subtitle="Visual Identity & Layouts" items={designProjects} />
        </div>

        <SkillsSection />
        <ContactSection />
      </main>
      <Footer />
      <style dangerouslySetInnerHTML={{ __html: `
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;400;700;900&display=swap');
        :root { --font-futura: "Futura", "Futura-Medium", "Futura PT", "Montserrat", "Segoe UI", system-ui, sans-serif; }
        body { font-family: var(--font-futura); background-color: #000; color: #fff; font-weight: 400; }
        p, .font-thin { font-weight: 100 !important; }
        
        /* Entrance Animations */
        @keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slide-up { from { transform: translateY(30px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        @keyframes slide-right { from { transform: translateX(-30px); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
        .animate-in { animation: slide-up 1s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
        .slide-in-from-right { animation-name: slide-right; }
        
        /* 2D Sketch Animations */
        @keyframes float-organic {
          0%, 100% { transform: translateY(0) rotate(-2deg); }
          50% { transform: translateY(-15px) rotate(3deg); }
        }
        .float-animation {
          animation: float-organic 6s ease-in-out infinite;
        }
        
        .sketch-path {
          stroke-dasharray: 400;
          stroke-dashoffset: 400;
          animation: draw-sketch 3.5s cubic-bezier(0.4, 0, 0.2, 1) infinite alternate;
        }
        .delay-1 { animation-delay: 0.3s; }
        .delay-2 { animation-delay: 0.6s; }
        .delay-3 { animation-delay: 0.9s; }
        
        @keyframes draw-sketch {
          0% { stroke-dashoffset: 400; opacity: 0; }
          10% { opacity: 1; }
          100% { stroke-dashoffset: 0; opacity: 1; }
        }

        /* Hide scrollbar for carousels but allow scrolling */
        .hide-scrollbar {
          -ms-overflow-style: none;  /* IE and Edge */
          scrollbar-width: none;  /* Firefox */
        }
        .hide-scrollbar::-webkit-scrollbar {
          display: none; /* Chrome, Safari and Opera */
        }

        /* Global scrollbar */
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-thumb { background: #222; border-radius: 10px; }
      `}} />
    </div>
  );
}