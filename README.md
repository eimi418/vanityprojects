# GEO Landing Page - Instrukcje wdrożenia

## 📋 Przegląd

Profesjonalny landing page dla projektu GEO (Generative Engine Optimization) zbudowany z:
- **Astro.js** - framework
- **Tailwind CSS** - styling
- **Netlify Forms** - obsługa formularza kontaktowego
- **Responsive Design** - w pełni responsywny dla wszystkich urządzeń

## 🚀 Szybki start

### 1. Przygotowanie plików

Skopiuj dostarczone pliki do swojego repo:

```bash
# Skopiuj nową stronę główną
cp index.astro src/pages/index.astro

# Skopiuj nowy layout
cp LandingLayout.astro src/layouts/LandingLayout.astro
```

### 2. Lokalne uruchomienie

```bash
# Zainstaluj zależności (jeśli jeszcze nie zrobiłeś)
npm install

# Uruchom serwer deweloperski
npm run dev

# Lub z Netlify CLI (zalecane dla testowania formularzy)
netlify dev
```

Strona będzie dostępna pod `http://localhost:4321` (lub `http://localhost:8888` z Netlify CLI)

### 3. Deploy na Netlify

#### Przez Git:

```bash
# Commitnij zmiany
git add .
git commit -m "Add GEO landing page"
git push origin main
```

Netlify automatycznie wykryje zmiany i zbuduje stronę.

#### Ręczny deploy:

```bash
# Zbuduj projekt
npm run build

# Deploy przez Netlify CLI
netlify deploy --prod
```

## 📧 Konfiguracja formularza

Formularz kontaktowy używa **Netlify Forms** i jest już skonfigurowany. Aby działał poprawnie:

### 1. Po pierwszym deploy

1. Przejdź do dashboardu Netlify: `https://app.netlify.com`
2. Wybierz swoją stronę
3. Przejdź do **Forms** w menu bocznym
4. Zobaczysz formularz `geo-contact` - jest gotowy do użycia!

### 2. Konfiguracja powiadomień email

1. W zakładce **Forms** → kliknij na `geo-contact`
2. Przejdź do **Form notifications**
3. Dodaj powiadomienie email:
   - **Email to notify**: Twój adres email
   - **Event to listen for**: New form submission

### 3. Opcjonalne: Własna strona podziękowania

Możesz dodać custom success page:

```astro
<!-- src/pages/thank-you.astro -->
---
import LandingLayout from '../layouts/LandingLayout.astro';
---

<LandingLayout title="Dziękujemy! | GEO">
	<section class="min-h-screen flex items-center justify-center bg-gradient-to-br from-purple-900 to-gray-900 text-white">
		<div class="text-center px-4">
			<h1 class="text-5xl font-bold mb-6">Dziękujemy!</h1>
			<p class="text-xl mb-8">Skontaktujemy się z Tobą w ciągu 24 godzin.</p>
			<a href="/" class="px-8 py-4 bg-purple-600 rounded-lg hover:bg-purple-700 transition">
				Powrót do strony głównej
			</a>
		</div>
	</section>
</LandingLayout>
```

Następnie w formularzu dodaj:
```html
<input type="hidden" name="success_redirect" value="/thank-you" />
```

## 🎨 Dostosowywanie

### Kolory

Główne kolory są zdefiniowane w Tailwind. Aby je zmienić:

```css
/* src/styles/globals.css */
:root {
  --color-purple-600: #9333ea;
  --color-pink-600: #db2777;
}
```

### Treść

Cała treść jest w pliku `src/pages/index.astro`. Każda sekcja jest oznaczona komentarzem:

```astro
<!-- Hero Section -->
<!-- Problem Section -->
<!-- Solution Section -->
<!-- Advantage Section -->
<!-- Why Now Section -->
<!-- Process Section -->
<!-- Team Section -->
<!-- Pricing Section -->
<!-- CTA Section -->
```

### Meta tagi SEO

Edytuj w `src/layouts/LandingLayout.astro`:

```astro
const { 
	title,
	description = "Twój własny opis"
} = Astro.props;
```

## 📱 Responsywność

Landing page jest w pełni responsywny z breakpointami:
- **Mobile**: < 640px
- **Tablet**: 640px - 1024px
- **Desktop**: > 1024px

## ⚡ Optymalizacja

### Core Web Vitals

Strona jest zoptymalizowana pod:
- **LCP** (Largest Contentful Paint): < 2.5s
- **FID** (First Input Delay): < 100ms
- **CLS** (Cumulative Layout Shift): < 0.1

### Obrazy

Jeśli dodajesz obrazy:

```astro
---
import { Image } from 'astro:assets';
import myImage from '../assets/my-image.jpg';
---

<Image src={myImage} alt="Opis" />
```

Astro automatycznie zoptymalizuje obrazy przez Netlify Image CDN.

## 🔧 Rozwiązywanie problemów

### Formularz nie działa lokalnie

To normalne! Netlify Forms działa tylko na produkcji lub przez `netlify dev`:

```bash
netlify dev
```

### Stylowanie się nie ładuje

Sprawdź czy Tailwind jest poprawnie skonfigurowany:

```bash
# Sprawdź czy plik istnieje
ls src/styles/globals.css

# Sprawdź import w layout
grep "globals.css" src/layouts/LandingLayout.astro
```

### Build errors

```bash
# Wyczyść cache i przebuduj
rm -rf node_modules .astro
npm install
npm run build
```

## 📊 Analityka

Aby dodać Google Analytics lub inne narzędzia:

```astro
<!-- src/layouts/LandingLayout.astro -->
<head>
	<!-- ... inne tagi ... -->
	
	<!-- Google Analytics -->
	<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
	<script>
		window.dataLayer = window.dataLayer || [];
		function gtag(){dataLayer.push(arguments);}
		gtag('js', new Date());
		gtag('config', 'GA_MEASUREMENT_ID');
	</script>
</head>
```

## 🎯 Następne kroki

1. ✅ Deploy na Netlify
2. ✅ Skonfiguruj powiadomienia email dla formularza
3. ✅ Dodaj Google Analytics (opcjonalnie)
4. ✅ Dostosuj treść do swoich potrzeb
5. ✅ Przetestuj na różnych urządzeniach
6. ✅ Skonfiguruj własną domenę w Netlify

## 💡 Wskazówki

- **SEO**: Dodaj sitemap.xml przez Astro sitemap integration
- **Performance**: Włącz Netlify's automatic image optimization
- **Security**: Dodaj Content Security Policy headers w netlify.toml
- **A/B Testing**: Użyj Netlify Edge Functions do testów A/B

## 📞 Support

Jeśli masz pytania:
1. Sprawdź [dokumentację Astro](https://docs.astro.build)
2. Sprawdź [dokumentację Netlify](https://docs.netlify.com)
3. Sprawdź [dokumentację Tailwind](https://tailwindcss.com/docs)

## 🎉 Gratulacje!

Twój landing page GEO jest gotowy! 🚀
