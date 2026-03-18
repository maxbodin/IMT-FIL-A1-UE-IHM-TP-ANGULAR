# IMT-FIL-A1-UE-IHM-TP-ANGULAR - Image Gallery Application

Interactive **Angular 19 standalone components dashboard** demonstrating image gallery with state management using RxJS. Built as a teaching project for IMT-FIL-A1 UE IHM course.

## 🎓 Learning Goals

This project demonstrates:
- Standalone Angular components (no NgModule)
- RxJS observables and BehaviorSubject
- Parent-child component communication (property binding, event emission, two-way binding)
- Reactive state management patterns
- Component isolation and reusability

## 🎯 Project Overview

This application showcases a four-grid layout dashboard with:
- **Grid 1:** Interactive timer with play/stop/reset controls
- **Grid 2:** Image gallery navigator with thumbnail grid
- **Grid 3:** Large image display area
- **Grid 5:** Image scale factor slider

**Tech Stack:**
- Angular 19.0.1 (standalone components, no NgModule)
- RxJS 7.8.0 (BehaviorSubject for reactive state)
- TypeScript 5.5.2
- Karma + Jasmine for testing
- Vanilla CSS Grid layout (no external UI libraries)

## 📁 Project Structure

```
src/app/
├── app.component.ts           # Main layout container (4-column grid)
├── app.component.html         # Dashboard layout with event bindings
├── app.config.ts              # Angular configuration (routing, zone detection)
├── grid1/                      # Timer component
│   ├── grid1.component.ts
│   └── grid1.component.html
├── grid2/                      # Image gallery navigator
│   ├── grid2.component.ts
│   └── grid2.component.html
├── grid3/                      # Large image display
│   ├── grid3.component.ts
│   └── grid3.component.html
├── grid5/                      # Scale slider control
│   ├── grid5.component.ts
│   └── grid5.component.html
└── services/
    ├── imageLibrary.ts        # Observable-based image state service
    └── timer.ts               # (Unused - kept for reference)
public/assets/images/          # Gallery images (7 PNG files)
```

## 🔄 Architecture & Data Flow

### State Management Pattern
- **ImageLibrary Service** (`services/imageLibrary.ts`): Single source of truth using RxJS BehaviorSubject
  - Maintains array of images with metadata (URL, scale factor)
  - Observable `currentImageObserver` broadcasts state changes
  - Singleton (providedIn: 'root')

### Component Communication
1. **Grid2** → emits `urlChange` event when image selection changes
2. **AppComponent** → receives event and updates `currentImageUrl`
3. **Grid3** → receives URL via property binding `[url]`
4. **Grid5** ↔ **AppComponent** → two-way binding `[(size)]` for scale factor

### Data Flow Diagram
```
ImageLibrary (BehaviorSubject)
    ↓
Grid2.currentImageObserver.subscribe()
    ↓
Grid2 emits (urlChange) 
    ↓
AppComponent.onUrlChange()
    ↓
Grid3 receives [url] binding
```

## 📝 Key Features

### Image Gallery (Grid2)
- 7-image collection from `assets/images/`
- Navigation buttons: First, Previous, Next, Last
- Thumbnail grid with click-to-select
- Responsive image sizing via slider

### Timer (Grid1)
- Local state management (no service dependency)
- Play/Stop/Reset controls with button state flags
- 1-second interval ticking

### Image Display (Grid3)
- Receives URL via property binding
- Responsive sizing based on Grid5 slider

### Scale Control (Grid5)
- Slider input with two-way binding
- Updates image size in real-time
