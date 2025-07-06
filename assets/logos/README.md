# 🎨 Assets & Branding CYBA Universe

## 📋 Vue d'Ensemble

Ce dossier contient les assets officiels de **CYBA Universe**, incluant logos, icônes, et éléments de branding pour la plateforme gaming Web3 de cybersécurité.

## 🎭 Logo Principal

### **CYBA Universe Logo**
- **Formats disponibles** : SVG, PNG (transparence), JPG
- **Variations** : Horizontal, vertical, icon seule
- **Couleurs** : Full color, monochrome, blanc
- **Tailles** : 16px à 2048px

### **Guidelines Logo**
```yaml
Usage Autorisé:
├── ✅ Communication officielle
├── ✅ Partenariats approuvés
├── ✅ Articles éducatifs (avec attribution)
├── ✅ Community content (non-commercial)
└── ✅ Intégrations techniques (API, widgets)

Usage Interdit:
├── ❌ Modification sans autorisation
├── ❌ Usage commercial non-autorisé
├── ❌ Association marques concurrentes
├── ❌ Contenus inappropriés/offensants
└── ❌ Prétendre affiliation officielle
```

## 🎮 Iconographie Gaming

### **Avatar Types Icons**
- **CYBER_ROOKIE** : Icône apprenti avec laptop
- **HACKER_ELITE** : Interface neurale stylisée
- **CYBER_GUARDIAN** : Bouclier cyber protecteur
- **MATRIX_WARRIOR** : Katana data épique
- **GHOST_OPERATIVE** : Fantôme digital discret
- **DATA_MYSTIC** : Staff quantique mystique
- **QUANTUM_ENGINEER** : Compilateur réalité
- **CYBORG_LEGEND** : Core infini légendaire

### **Equipment Rarity Colors**
```css
/* Couleurs rareté équipements */
.rarity-common { color: #6B7280; }      /* Gris */
.rarity-uncommon { color: #10B981; }    /* Vert */
.rarity-rare { color: #3B82F6; }        /* Bleu */
.rarity-epic { color: #8B5CF6; }        /* Violet */
.rarity-legendary { color: #F59E0B; }   /* Orange */
.rarity-mythic { color: #EF4444; }      /* Rouge */
.rarity-cosmic { 
  background: linear-gradient(45deg, #F59E0B, #EF4444, #8B5CF6, #3B82F6);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}
```

## 🌈 Palette de Couleurs

### **Couleurs Primaires**
```yaml
Cyber Cyan:
├── Primary: #06B6D4 (cyan-500)
├── Light: #67E8F9 (cyan-300)
├── Dark: #0E7490 (cyan-700)
└── Glow: rgba(6, 182, 212, 0.5)

Gaming Purple:
├── Primary: #8B5CF6 (violet-500)
├── Light: #C4B5FD (violet-300)
├── Dark: #5B21B6 (violet-800)
└── Glow: rgba(139, 92, 246, 0.5)

Matrix Green:
├── Primary: #10B981 (emerald-500)
├── Light: #6EE7B7 (emerald-300)
├── Dark: #047857 (emerald-700)
└── Glow: rgba(16, 185, 129, 0.5)
```

### **Couleurs Secondaires**
```yaml
Neural Pink:
├── Primary: #EC4899 (pink-500)
├── Light: #F9A8D4 (pink-300)
└── Dark: #BE185D (pink-700)

Quantum Orange:
├── Primary: #F59E0B (amber-500)
├── Light: #FCD34D (amber-300)
└── Dark: #D97706 (amber-600)

Deep Space:
├── Background: #0F172A (slate-900)
├── Surface: #1E293B (slate-800)
├── Border: #334155 (slate-700)
└── Text: #F1F5F9 (slate-100)
```

## 🎨 Style Guidelines

### **Typography Gaming**
```css
/* Fonts principales */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&display=swap');

.font-gaming-title {
  font-family: 'Inter', sans-serif;
  font-weight: 800; /* font-black */
  letter-spacing: -0.025em; /* tracking-tight */
  background: linear-gradient(to right, #06B6D4, #8B5CF6);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}

.font-gaming-mono {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 500;
  color: #10B981; /* text-emerald-500 */
}
```

### **Effets Visuels Signature**
```css
/* Glass morphism gaming */
.glass-cyber {
  backdrop-filter: blur(16px);
  background: rgba(15, 23, 42, 0.8); /* slate-900/80 */
  border: 1px solid rgba(6, 182, 212, 0.3); /* cyan-500/30 */
  box-shadow: 0 8px 32px rgba(6, 182, 212, 0.1);
}

/* Glow effects */
.glow-cyan {
  box-shadow: 
    0 0 20px rgba(6, 182, 212, 0.3),
    0 0 40px rgba(6, 182, 212, 0.1);
}

.glow-purple {
  box-shadow: 
    0 0 20px rgba(139, 92, 246, 0.3),
    0 0 40px rgba(139, 92, 246, 0.1);
}

/* Animations gaming */
@keyframes float-gentle {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-6px); }
}

@keyframes pulse-glow {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}

.animate-float { animation: float-gentle 6s ease-in-out infinite; }
.animate-pulse-glow { animation: pulse-glow 2s ease-in-out infinite; }
```

## 📱 Assets Responsifs

### **Logo Sizes Recommandées**
```yaml
Favicon: 16x16, 32x32, 48x48
App Icons: 128x128, 256x256, 512x512
Social Media:
├── Twitter: 400x400
├── Discord: 512x512
├── LinkedIn: 300x300
└── OpenGraph: 1200x630

Print/High-res: 2048x2048, 4096x4096
```

### **Breakpoints Design**
```css
/* Responsive gaming design */
@media (max-width: 640px) {
  .logo-mobile { max-width: 120px; }
  .text-gaming { font-size: 1.5rem; }
}

@media (min-width: 641px) and (max-width: 1024px) {
  .logo-tablet { max-width: 200px; }
  .text-gaming { font-size: 2rem; }
}

@media (min-width: 1025px) {
  .logo-desktop { max-width: 300px; }
  .text-gaming { font-size: 2.5rem; }
}
```

## 🎯 Usage Brand

### **Ton & Voice Gaming**
- **Énergique** : Dynamisme et action
- **Technique** : Expertise cybersécurité
- **Inclusif** : Communauté accueillante
- **Innovant** : Technologies de pointe
- **Ludique** : Gaming et fun

### **Vocabulaire CYBA**
```yaml
Termes Gaming Signature:
├── "Cyber Warriors" : Étudiants/utilisateurs
├── "Combat Drills" : Exercices pratiques
├── "Data Fortress" : Infrastructure sécurisée
├── "Digital Arsenal" : Outils cybersécurité
├── "Quantum Leap" : Innovation technologique
├── "Neural Network" : Communauté connectée
└── "Cyber Legends" : Experts reconnus
```

## 📄 Licences & Permissions

### **Assets Usage Rights**
```yaml
Documentation Publique:
├── License: CC BY-NC-SA 4.0
├── Usage: Attribution non-commerciale
├── Modifications: Autorisées avec attribution
└── Distribution: Autorisée sous même licence

Brand Assets:
├── Propriété: CYBA Universe SAS
├── Usage: Autorisation requise
├── Commercial: Contact partnerships@cyba-universe.com
└── Modifications: Interdites sans autorisation
```

### **Attribution Requise**
```html
<!-- Exemple attribution -->
<footer>
  Powered by <a href="https://cyba-universe.com">CYBA Universe</a>
  <!-- Logo avec lien si utilisation logo -->
</footer>
```

## 📞 Contact Assets

### **Demandes Spéciales**
- **🎨 Custom Assets** : design@cyba-universe.com
- **🤝 Partnerships** : partnerships@cyba-universe.com
- **📄 Licences** : legal@cyba-universe.com
- **🚀 Press Kit** : press@cyba-universe.com

### **Formats Disponibles**
- **Vectoriel** : SVG, AI, EPS
- **Raster** : PNG (transparence), JPG, WebP
- **Animation** : GIF, MP4, Lottie
- **Print** : PDF, TIFF haute résolution

---

## 🎮 Exemples d'Usage

### **Hero Section**
```jsx
<div className="hero-section glass-cyber">
  <img src="/assets/logos/cyba-universe-logo.svg" 
       alt="CYBA Universe" 
       className="logo-desktop animate-float" />
  <h1 className="font-gaming-title text-4xl">
    Forge Your Cyber Legend
  </h1>
</div>
```

### **Avatar Card**
```jsx
<div className="avatar-card glow-purple">
  <img src="/assets/avatars/cyber-rookie-icon.svg" 
       alt="Cyber Rookie" 
       className="w-12 h-12" />
  <span className="font-gaming-mono text-emerald-400">
    CYBER ROOKIE
  </span>
</div>
```

---

*Ces assets représentent l'identité visuelle de CYBA Universe. Utilisez-les avec respect pour maintenir la cohérence de notre marque gaming ! 🎮*