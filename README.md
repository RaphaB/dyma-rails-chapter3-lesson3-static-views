# EShop - Vues statiques HTML/Tailwind CSS

Ce dossier contient toutes les vues statiques HTML pour le projet EShop, stylisées avec Tailwind CSS.

## 📁 Liste des pages

### Pages publiques

1. **index.html** - Page d'accueil
   - Hero section avec appel à l'action
   - Catégories populaires (Électronique, Vêtements, Livres, Maison & Jardin)
   - Produits en vedette
   - Navigation complète et footer

2. **products.html** - Catalogue de produits
   - Barre latérale avec filtres (catégorie, prix, disponibilité)
   - Grille de produits avec pagination
   - Barre de tri (popularité, prix, nouveautés)
   - Badge de stock (en stock, stock limité, rupture de stock)

3. **product-detail.html** - Page détaillée d'un produit
   - Galerie d'images avec miniatures
   - Informations produit (prix, description, caractéristiques)
   - Sélecteur de quantité
   - Système d'avis clients avec notation
   - Distribution des notes (graphique à barres)
   - Liste des avis avec dates

4. **cart.html** - Panier d'achat
   - Liste des articles avec gestion de quantité
   - Récapitulatif de commande (sous-total, TVA, total)
   - Code promo
   - Bouton de paiement
   - État vide du panier (commenté)

5. **checkout.html** - Page de paiement
   - Indicateur de progression (3 étapes)
   - Formulaire d'informations de livraison
   - Sélection du mode de paiement (carte bancaire, PayPal)
   - Zone Stripe Elements (placeholder)
   - Récapitulatif de commande

### Pages d'authentification

6. **login.html** - Connexion
   - Formulaire de connexion (email, mot de passe)
   - Option "Se souvenir de moi"
   - Lien de récupération de mot de passe
   - Connexion sociale (Google, Facebook)

7. **signup.html** - Inscription
   - Formulaire d'inscription complet
   - Acceptation des CGV
   - Newsletter opt-in
   - Connexion sociale (Google, Facebook)
   - Avantages de l'inscription

### Espace client

8. **profile.html** - Profil utilisateur
   - Navigation latérale (profil, commandes, favoris, déconnexion)
   - Formulaire d'informations personnelles
   - Gestion des adresses (principale, secondaire)
   - Changement de mot de passe

9. **orders.html** - Liste des commandes
   - Filtres par statut
   - Barre de recherche
   - Cartes de commande avec informations détaillées
   - Badges de statut colorés (livrée, expédiée, en attente, annulée)
   - Actions par commande (détails, facture, recommander)
   - Pagination

10. **order-detail.html** - Détail d'une commande
    - Timeline de statut avec icônes
    - Liste des articles commandés
    - Adresse de livraison
    - Récapitulatif financier
    - Mode de paiement
    - Actions (facture, recommander, support)

## 🎨 Fonctionnalités UI

### Composants communs

- **Navigation** : Logo, menu, recherche, panier avec badge, icône profil
- **Footer** : 4 colonnes (présentation, liens, compte, aide)
- **Breadcrumb** : Fil d'Ariane pour la navigation
- **Filtres** : Checkboxes et inputs pour affiner les recherches
- **Pagination** : Boutons de navigation entre pages
- **Cartes produit** : Image, titre, prix, notation, stock, bouton d'ajout

### Design patterns

- **Responsive** : Layout adaptatif mobile/tablette/desktop (grilles Tailwind)
- **État vide** : Messages pour panier vide, aucun résultat
- **États de stock** : En stock (vert), stock limité (orange), rupture (rouge/gris)
- **États de commande** : Badges colorés selon le statut
- **Formulaires** : Focus states, validation visuelle
- **Notifications** : Zones d'information colorées (info, succès, warning)

## 🛠️ Technologies utilisées

- **HTML5** : Structure sémantique
- **Tailwind CSS** : via CDN (https://cdn.tailwindcss.com)
- **Heroicons** : Icônes SVG intégrées
- **Stripe.js** : Script de paiement (checkout.html)

## 📖 Comment utiliser ces vues

### 1. Prévisualisation

Vous pouvez ouvrir chaque fichier HTML directement dans votre navigateur :

```bash
# Ouvrir dans le navigateur par défaut
open static-views/index.html

# Ou utilisez un serveur local pour une meilleure expérience
python -m http.server 8000
# Puis ouvrez http://localhost:8000/static-views/
```

### 2. Intégration dans Rails

Pour implémenter ces vues dans votre application Rails :

#### a) Structure de fichiers Rails

```
app/views/
├── layouts/
│   ├── application.html.erb        # À partir de la navigation/footer
│   └── _navigation.html.erb
│   └── _footer.html.erb
├── home/
│   └── index.html.erb              # index.html
├── products/
│   ├── index.html.erb              # products.html
│   └── show.html.erb               # product-detail.html
├── carts/
│   └── show.html.erb               # cart.html
├── checkouts/
│   └── new.html.erb                # checkout.html
├── sessions/
│   └── new.html.erb                # login.html
├── registrations/
│   └── new.html.erb                # signup.html
├── users/
│   └── show.html.erb               # profile.html
└── orders/
    ├── index.html.erb              # orders.html
    └── show.html.erb               # order-detail.html
```

#### b) Installation de Tailwind CSS dans Rails

Votre Rails 8 utilise déjà Tailwind CSS. Assurez-vous que la configuration est correcte :

```bash
# Vérifier que Tailwind est installé
rails tailwindcss:install

# Le fichier de configuration devrait être :
# config/tailwind.config.js
```

#### c) Conversion HTML → ERB

1. **Remplacer les liens statiques par des helpers Rails** :

```erb
<!-- Avant (HTML statique) -->
<a href="products.html">Produits</a>

<!-- Après (ERB) -->
<a href="<%= products_path %>">Produits</a>
```

2. **Utiliser les données dynamiques** :

```erb
<!-- Avant -->
<h1>MacBook Pro 14"</h1>

<!-- Après -->
<h1><%= @product.name %></h1>
```

3. **Boucles pour les listes** :

```erb
<!-- Avant (produits en dur) -->
<div class="product-card">...</div>
<div class="product-card">...</div>

<!-- Après -->
<% @products.each do |product| %>
  <div class="product-card">
    <h3><%= product.name %></h3>
    <p><%= number_to_currency(product.price) %></p>
  </div>
<% end %>
```

4. **Formulaires Rails** :

```erb
<!-- Avant (HTML statique) -->
<form>
  <input type="text" name="email">
  <button>Submit</button>
</form>

<!-- Après (form_with) -->
<%= form_with model: @user, local: true do |f| %>
  <%= f.email_field :email, class: "w-full px-4 py-3..." %>
  <%= f.submit "S'inscrire", class: "w-full bg-indigo-600..." %>
<% end %>
```

#### d) Assets et images

Les placeholders "Image produit" doivent être remplacés par :

```erb
<%= image_tag @product.images.first,
    class: "w-full h-64 object-cover rounded-lg",
    alt: @product.name %>
```

#### e) Partials pour réutilisation

Créez des partials pour les composants réutilisables :

```erb
<!-- app/views/products/_product_card.html.erb -->
<div class="bg-white border border-gray-200 rounded-lg...">
  <%= image_tag product.images.first %>
  <h3><%= link_to product.name, product_path(product) %></h3>
  <p><%= number_to_currency(product.price) %></p>
  <%= button_to "Ajouter au panier",
      cart_items_path(product_id: product.id),
      class: "bg-indigo-600 text-white..." %>
</div>

<!-- Utilisation -->
<% @products.each do |product| %>
  <%= render 'products/product_card', product: product %>
<% end %>
```

## 🎯 Points d'attention pour l'implémentation

### 1. Navigation dynamique

- Le badge du panier doit afficher `<%= current_user&.cart_items&.sum(:quantity) || 0 %>`
- Afficher/masquer les liens selon `user_signed_in?`

### 2. Filtres et recherche

- Les filtres doivent utiliser `form_with` avec `method: :get`
- Conserver les paramètres de filtres dans l'URL
- Utiliser Ransack ou des scopes pour la logique de filtrage

### 3. Pagination

- Utiliser Pagy gem comme spécifié
- Remplacer les boutons par `<%= pagy_nav(@pagy) %>`
- Personnaliser les styles Pagy pour correspondre à Tailwind

### 4. Stripe Integration

- Le placeholder Stripe Elements doit être remplacé par le vrai composant
- Suivre la documentation Stripe pour `checkout.html`

### 5. États et statuts

Utiliser des helpers pour les badges de statut :

```ruby
# app/helpers/orders_helper.rb
def order_status_badge(order)
  colors = {
    'pending' => 'bg-yellow-100 text-yellow-800',
    'paid' => 'bg-blue-100 text-blue-800',
    'shipped' => 'bg-blue-100 text-blue-800',
    'delivered' => 'bg-green-100 text-green-800',
    'cancelled' => 'bg-red-100 text-red-800'
  }

  content_tag :span,
    t("orders.status.#{order.status}"),
    class: "px-3 py-1 rounded-full text-sm font-semibold #{colors[order.status]}"
end
```

### 6. Traductions (i18n)

Remplacer les textes en dur par des clés de traduction :

```erb
<!-- Avant -->
<h1>Mes Commandes</h1>

<!-- Après -->
<h1><%= t('.title') %></h1>
```

```yaml
# config/locales/fr.yml
fr:
  orders:
    index:
      title: "Mes Commandes"
```

## 📝 Checklist d'implémentation

- [ ] Installer et configurer Tailwind CSS
- [ ] Créer les layouts (application, navigation, footer)
- [ ] Convertir chaque page HTML en vue ERB
- [ ] Remplacer les liens par des path helpers
- [ ] Implémenter les formulaires avec form_with
- [ ] Créer les partials pour composants réutilisables
- [ ] Intégrer Active Storage pour les images
- [ ] Configurer Pagy pour la pagination
- [ ] Implémenter les filtres et la recherche (Ransack)
- [ ] Ajouter les helpers pour badges et statuts
- [ ] Intégrer Stripe Elements
- [ ] Ajouter les traductions i18n
- [ ] Tester la responsivité sur mobile/tablette
- [ ] Implémenter Hotwire (Turbo/Stimulus) pour l'interactivité

## 🚀 Prochaines étapes

1. **Phase 1 : Structure de base**
   - Layout principal avec navigation et footer
   - Page d'accueil
   - Catalogue de produits

2. **Phase 2 : Interactivité**
   - Panier dynamique avec Turbo Streams
   - Filtres en temps réel avec Stimulus
   - Badge de panier mis à jour automatiquement

3. **Phase 3 : Authentification et commandes**
   - Formulaires de login/signup
   - Profil utilisateur
   - Historique et détail des commandes

4. **Phase 4 : Paiement**
   - Intégration Stripe complète
   - Webhooks pour confirmation de paiement

## 💡 Astuces

- **Stimulus Controllers** : Créez des contrôleurs Stimulus pour :
  - Galerie d'images (product-detail)
  - Gestion de quantité (cart)
  - Recherche instantanée (products)

- **Turbo Frames** : Utilisez des Turbo Frames pour :
  - Mise à jour du panier sans rechargement
  - Filtres de produits
  - Pagination

- **ViewComponents** : Considérez l'utilisation de ViewComponents pour :
  - Cartes produit
  - Badges de statut
  - Navigation latérale (profil)

## 📚 Ressources

- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Rails Views Guide](https://guides.rubyonrails.org/action_view_overview.html)
- [Hotwire Documentation](https://hotwired.dev/)
- [Stripe Elements](https://stripe.com/docs/stripe-js)
- [Pagy Documentation](https://ddnexus.github.io/pagy/)

---

**Bonne implémentation !** 🎉

Si vous avez des questions ou besoin d'aide pour l'intégration Rails, n'hésitez pas.
