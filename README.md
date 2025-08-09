# Consigne à Bagages Rouen

Application web complète de consigne à bagages pour Rouen avec SEO local optimisé, système de réservation et paiement Stripe.

## 🚀 Fonctionnalités

- **Réservation en ligne** : Interface intuitive avec sélection de dates/heures
- **Paiement sécurisé** : Intégration Stripe Checkout complète
- **SEO local optimisé** : Pages dédiées pour Rouen gare, centre-ville
- **Multilingue** : Support FR/EN avec hreflang
- **Admin dashboard** : Interface d'administration pour gérer les prix et créneaux
- **E-mails automatiques** : Confirmations avec QR codes
- **Design responsive** : Mobile-first, score Lighthouse ≥ 95

## 🛠 Stack technique

- **Framework** : Next.js 14 (App Router) + TypeScript
- **UI** : Tailwind CSS + shadcn/ui
- **Base de données** : SQLite + Prisma ORM
- **Paiements** : Stripe Checkout
- **E-mails** : Resend / Nodemailer
- **QR Codes** : qrcode library
- **Déploiement** : Vercel ready

## 📦 Installation

1. **Cloner et installer les dépendances**
```bash
git clone [repo]
cd consigne-bagages-rouen
npm install
```

2. **Configuration de l'environnement**
```bash
cp .env.example .env
```

Remplir les variables dans `.env` :

### Variables obligatoires
```bash
# Database
DATABASE_URL="file:./dev.db"

# Stripe
STRIPE_SECRET_KEY=sk_test_votre_cle_secrete_stripe
STRIPE_WEBHOOK_SECRET=whsec_votre_secret_webhook
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_votre_cle_publique_stripe

# Admin
ADMIN_PASSWORD=votre_mot_de_passe_admin_securise

# Site
SITE_URL=http://localhost:3000
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### Variables optionnelles
```bash
# Email (choisir Resend OU SMTP)
RESEND_API_KEY=re_votre_cle_resend
# OU
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=votre@email.com
SMTP_PASS=votre_mot_de_passe_app

# Analytics
NEXT_PUBLIC_GOOGLE_ANALYTICS_ID=GA_MEASUREMENT_ID
```

3. **Initialiser la base de données**
```bash
npx prisma migrate dev
npx prisma db seed
```

4. **Lancer en développement**
```bash
npm run dev
```

## 🎯 Configuration Stripe

1. **Créer un compte Stripe** : https://dashboard.stripe.com/register

2. **Récupérer les clés API** dans le dashboard Stripe :
   - Clé secrète (commence par `sk_test_`)
   - Clé publique (commence par `pk_test_`)

3. **Configurer le webhook** pour les paiements :
```bash
# Terminal 1 - Lancer l'app
npm run dev

# Terminal 2 - Écouter les webhooks Stripe
npm run stripe:listen
```

4. **URL du webhook en production** : `https://votre-domaine.com/api/stripe/webhook`

## 🏗 Structure du projet

```
├── app/                          # Pages Next.js App Router
│   ├── api/                      # API Routes
│   │   ├── calculate-price/      # Calcul des prix
│   │   ├── reservations/         # CRUD réservations
│   │   └── stripe/webhook/       # Webhook Stripe
│   ├── reservation/              # Page de réservation
│   ├── consigne-bagages-rouen-gare/ # Page SEO gare
│   └── consigne-rouen-centre/    # Page SEO centre
├── components/                   # Composants réutilisables
│   ├── Header.tsx
│   ├── Footer.tsx
│   └── ui/                      # shadcn/ui components
├── lib/                         # Utilitaires
│   ├── prisma.ts               # Client Prisma
│   ├── stripe.ts               # Client Stripe
│   ├── pricing.ts              # Logique tarification
│   ├── email.ts                # Service e-mail
│   └── qr-code.ts              # Génération QR codes
└── prisma/                     # Schéma base de données
    ├── schema.prisma
    └── seed.ts
```

## 🎨 Pages principales

- **/** : Page d'accueil avec SEO local
- **/reservation** : Interface de réservation
- **/consigne-bagages-rouen-gare** : Page SEO dédiée gare
- **/consigne-rouen-centre** : Page SEO centre-ville
- **/tarifs** : Grille tarifaire
- **/admin** : Interface d'administration
- **/en** : Version anglaise

## 💰 Tarification par défaut

| Taille | Heure | Jour | Semaine |
|--------|-------|------|---------|
| S      | 6€    | 12€  | 60€     |
| M      | 8€    | 16€  | 80€     |
| L      | 12€   | 24€  | 120€    |
| XL     | 18€   | 36€  | 180€    |

**Suppléments** :
- Nuit (20h-8h) : +20%
- Jours fériés/WE : +30%
- Assurance renforcée : +5€

## 🔧 Commandes utiles

```bash
# Développement
npm run dev                    # Lancer en dev
npm run build                  # Build production
npm run start                  # Démarrer en production

# Base de données
npm run db:migrate             # Appliquer migrations
npm run db:seed                # Peupler avec données test
npm run db:reset               # Reset complet

# Stripe
npm run stripe:listen          # Écouter webhooks en local
```

## 🚀 Déploiement

### Vercel (recommandé)

1. **Connecter le repo** à Vercel
2. **Variables d'environnement** : Copier depuis `.env`
3. **Build command** : `npm run build`
4. **Configurer le webhook Stripe** : `https://votre-app.vercel.app/api/stripe/webhook`

### Autres plateformes

L'app est compatible avec tout hébergeur supportant Node.js :
- Railway
- Render
- DigitalOcean App Platform
- OVH Cloud

## 🔒 Interface Admin

Accès : `/admin` avec le mot de passe défini dans `ADMIN_PASSWORD`

**Fonctionnalités** :
- Gérer les tarifs par taille
- Créer/modifier les codes promo
- Voir les réservations
- Export CSV
- Gérer les créneaux disponibles

## 📧 Configuration e-mails

### Option 1 : Resend (recommandé)
```bash
RESEND_API_KEY=re_votre_cle_api
```

### Option 2 : SMTP (Gmail, Outlook, etc.)
```bash
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=votre@gmail.com
SMTP_PASS=mot_de_passe_application
```

## 🎯 SEO et performance

- **Score Lighthouse** : ≥ 95 sur tous les critères
- **Schema.org** : LocalBusiness, FAQPage, Product
- **Meta tags** : Open Graph, Twitter Cards
- **Hreflang** : FR/EN
- **Sitemap** : Généré automatiquement
- **Images optimisées** : Next.js Image component

## 🔍 Pages SEO locales

Mots-clés ciblés :
- "consigne à bagages Rouen"
- "consigne bagages gare Rouen" 
- "left luggage Rouen"
- "locker Rouen centre"
- "déposer bagages Rouen"

## 🐛 Dépannage

### Erreur Prisma
```bash
npx prisma generate
npx prisma db push
```

### Webhook Stripe non reçus
1. Vérifier `STRIPE_WEBHOOK_SECRET`
2. Relancer `stripe listen`
3. Vérifier l'URL webhook en production

### E-mails non envoyés
1. Vérifier les variables SMTP/Resend
2. Tester avec un service e-mail de dev
3. Vérifier les logs serveur

## 📞 Support

Pour toute question technique :
- Issues GitHub
- Documentation Stripe : https://stripe.com/docs
- Documentation Prisma : https://prisma.io/docs

---

**Développé avec ❤️ pour Rouen**