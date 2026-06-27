<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Star Max+ | La Super-App du Divertissement et des Talents</title>
    <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
    
    <!-- Script de traduction universelle (Bilinguisme automatique) -->
    <script type="text/javascript">
        function googleTranslateElementInit() {
            new google.translate.TranslateElement({
                pageLanguage: 'fr', 
                includedLanguages: 'en,fr,es,de', 
                layout: google.translate.TranslateElement.InlineLayout.SIMPLE, 
                autoDisplay: true
            }, 'google_translate_element');
        }
    </script>
    <script type="text/javascript" src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>

    <style>
        :root {
            --primary: #ffcc00;
            --dark: #0b0b0b;
            --surface: #141414;
            --text: #ffffff;
            --text-muted: #8c8c8c;
            --success: #00e676;
            --danger: #ff1744;
        }
        * { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI', Arial, sans-serif; }
        body { background-color: var(--dark); color: var(--text); overflow-x: hidden; }
        
        header {
            background-color: #000;
            padding: 15px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #222;
            position: sticky; top:0; z-index:100;
        }
        .logo-container img { height: 45px; width: auto; object-fit: contain; }
        .logo-text { font-size: 26px; font-weight: 900; letter-spacing: 1px; }
        .logo-text span { color: var(--primary); }

        /* BANDE PASSANTE TYPE CHAINE D'INFO (Ticker) */
        .ticker-wrap { width: 100%; background: var(--danger); border-bottom: 2px solid var(--primary); overflow: hidden; height: 35px; display: flex; align-items: center; }
        .ticker-title { background: var(--primary); color: #000; font-weight: bold; padding: 0 20px; height: 100%; display: flex; align-items: center; font-size: 13px; z-index: 10; font-weight: 800; text-transform: uppercase; white-space: nowrap; }
        .ticker { display: flex; white-space: nowrap; padding-left: 100%; animation: ticker 25s linear infinite; }
        .ticker-item { display: inline-block; padding: 0 30px; font-size: 14px; font-weight: 600; color: white; }
        @keyframes ticker {
            0% { transform: translate3d(0, 0, 0); }
            100% { transform: translate3d(-100%, 0, 0); }
        }

        /* Barre des 20 chaînes */
        .category-bar { display: flex; gap: 10px; padding: 15px 5%; overflow-x: auto; background: #000; white-space: nowrap; }
        .category-btn { background: var(--surface); color: white; border: 1px solid #333; padding: 8px 18px; border-radius: 20px; cursor: pointer; font-size: 14px; font-weight: 600; transition: all 0.3s; }
        .category-btn:hover, .category-btn.active { background: var(--primary); color: black; border-color: var(--primary); }

        .app-container { padding: 30px 5%; max-width: 1400px; margin: 0 auto; }
        .main-grid { display: grid; grid-template-columns: 2fr 1fr; gap: 30px; }
        @media (max-width: 992px) { .main-grid { grid-template-columns: 1fr; } }

        /* Régie de diffusion */
        .player-box { background: var(--surface); border-radius: 12px; padding: 15px; border: 1px solid #222; }
        .video-wrapper { position: relative; padding-bottom: 56.25%; height: 0; background: #000; border-radius: 8px; overflow: hidden; }
        .video-wrapper iframe { position: absolute; top:0; left:0; width:100%; height:100%; border:none; }

        .section-title { font-size: 22px; margin: 30px 0 15px 0; display: flex; justify-content: space-between; align-items: center; border-left: 4px solid var(--primary); padding-left: 10px; text-transform: uppercase; letter-spacing: 0.5px; }
        .grid-layout { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px; }
        
        /* Grille des Médias */
        .content-card { background: var(--surface); border-radius: 8px; overflow:hidden; border: 1px solid #222; transition: transform 0.3s; }
        .content-card:hover { transform: scale(1.02); border-color: var(--primary); }
        .card-thumb { width:100%; height:160px; background:#222; display:flex; align-items:center; justify-content:center; color:var(--text-muted); font-weight:bold; position: relative; background-size: cover; background-position: center; }
        .card-badge { position:absolute; top:10px; left:10px; background:rgba(0,0,0,0.8); padding:3px 8px; font-size:11px; border-radius:4px; border: 1px solid var(--primary); }
        .card-details { padding: 15px; }

        /* Blocs Commerciaux Latéraux */
        .sidebar-box { background: var(--surface); border-radius: 12px; padding: 20px; border: 1px solid #222; margin-bottom: 20px; }
        .btn-action { display:block; width:100%; background:var(--primary); color:black; text-align:center; padding:12px; border-radius:8px; font-weight:bold; text-decoration:none; margin-top:15px; transition: opacity 0.2s; }
        .btn-action:hover { opacity: 0.9; }
        .btn-bet { background: var(--success); color: black; }

        /* Espace Bannières Pub */
        .ad-banner { width: 100%; height: auto; min-height: 95px; background: #131313; margin-bottom: 25px; border: 1px dashed #333; border-radius: 8px; display: flex; align-items: center; justify-content: center; overflow: hidden; }
        .ad-banner img { width: 100%; height: auto; object-fit: cover; }
    </style>
</head>
<body>

    <header>
        <!-- Gestion Dynamique du Logo officiel -->
        <div class="logo-container">
            {% if monetization.links.logo_url %}
                <img src="{{ monetization.links.logo_url }}" alt="Logo Star Max+">
            {% else %}
                <div class="logo-text">Star Max<span>+</span></div>
            {% endif %}
        </div>
        <div style="display: flex; align-items: center; gap: 15px;">
            <div id="google_translate_element"></div>
            <a href="/admin/" style="color: white; text-decoration: none; font-size: 14px; border: 1px solid #333; padding: 5px 10px; border-radius: 4px;">Régie Équipe</a>
        </div>
    </header>

    <!-- BANDE PASSANTE EN DIRECT (FLASH INFO & PUB ENTREPRISES) -->
    <div class="ticker-wrap">
        <div class="ticker-title">Flash Info / Annonces</div>
        <div class="ticker">
            <span class="ticker-item">🔥 {{ ticker.news.line1 }}</span>
            <span class="ticker-item">📢 {{ ticker.news.line2 }}</span>
            <span class="ticker-item">⚡ {{ ticker.news.line3 }}</span>
        </div>
    </div>

    <!-- Sélecteur des 20 chaînes TV et Radio -->
    <div class="category-bar">
        <button class="category-btn active" onclick="switchChannel('TON_ID_LIVE_GENERAL')">📺 Star Max TV (Direct)</button>
        <button class="category-btn" onclick="switchChannel('ID_FLUX_CINEMA')">🎬 Star Max Cinéma</button>
        <button class="category-btn" onclick="switchChannel('ID_FLUX_SPORT')">⚽ Star Max Sport</button>
        <button class="category-btn" onclick="switchChannel('ID_FLUX_MUSIC')">🎵 Star Max Music</button>
        <button class="category-btn" onclick="switchChannel('ID_FLUX_WILD')">🐗 Star Max Wild</button>
        <button class="category-btn" onclick="switchChannel('ID_FLUX_ACTION')">🔥 Star Max Action</button>
        <button class="category-btn" onclick="switchChannel('ID_FLUX_RADIO')">📻 Star Max FM</button>
    </div>

    <div class="app-container">
        
        <!-- REGIE PUBLICITAIRE : GRANDE BANNIERE DU SITE -->
        <div class="ad-banner">
            {% for ad in collections.ads | reverse | limit(1) %}
            <a href="{{ ad.data.ad_url }}" target="_blank" style="width: 100%;">
                <img src="{{ ad.data.image }}" alt="Publicité {{ ad.data.title }}">
            </a>
            {% else %}
            <p style="color: #444; font-size: 14px;">Espace Publicitaire Privé Star Max+ (Contactez la régie commerciale)</p>
            {% endfor %}
        </div>

        <div class="main-grid">
            
            <!-- CONTENUS PRINCIPAUX -->
            <div>
                <div class="player-box">
                    <div class="video-wrapper">
                        <iframe id="main-player" src="https://www.youtube.com/embed/live_stream?channel=TON_ID_CANAL_PRINCIPAL" allowfullscreen></iframe>
                    </div>
                    <h2 id="channel-title" style="margin-top:15px; font-size:20px;">Star Max TV en Direct</h2>
                    <p style="color:var(--text-muted); font-size:14px;">L'application tout-en-un de l'écosystème Star Max</p>
                </div>

                <!-- VIDEOS À LA DEMANDE (VOD) -->
                <h3 class="section-title">Catalogue Vidéos & Émissions</h3>
                <div class="grid-layout">
                    {% for video in collections.videos | reverse %}
                    <div class="content-card">
                        <div class="card-thumb" style="background-image: url('{{ video.data.thumbnail }}')">
                            <span class="card-badge">{{ video.data.category }}</span>
                            {% if video.data.premium %}<span class="card-badge" style="left:auto; right:10px; background:var(--primary); color:black; font-weight:bold;">PREMIUM</span>{% endif %}
                        </div>
                        <div class="card-details">
                            <h4 style="margin-bottom: 10px;">{{ video.data.title }}</h4>
                            <p style="font-size: 13px; color: var(--text-muted); min-height: 40px;">{{ video.data.body | truncate(80) }}</p>
                            <a href="{% if video.data.premium %}{{ monetization.links.cinema_url }}{% else %}{{ video.data.video_url }}{% endif %}" class="btn-action" style="padding: 6px; font-size: 12px;">
                                {% if video.data.premium %}🔒 Débloquer ({{ monetization.links.cinema_price }}){% else %}▶️ Visionner Replay{% endif %}
                            </a>
                        </div>
                    </div>
                    {% endfor %}
                </div>

                <!-- FIL D'ACTUALITÉS -->
                <h3 class="section-title">Actualités & Info (Star Max News)</h3>
                <div class="grid-layout">
                    {% for article in collections.articles | reverse %}
                    <div class="content-card">
                        <div class="card-thumb" style="background-image: url('{{ article.data.image }}')">
                            <span class="card-badge">{{ article.data.category }}</span>
                        </div>
                        <div class="card-details">
                            <span style="font-size: 11px; color: var(--primary);">{{ article.data.date | date('DD/MM/YYYY') }}</span>
                            <h4 style="margin: 5px 0 10px 0;">{{ article.data.title }}</h4>
                            <p style="font-size: 12px; color: var(--text-muted);">Par {{ article.data.author }}</p>
                        </div>
                    </div>
                    {% endfor %}
                </div>
            </div>

            <!-- STRUCTURES MONÉTIQUES & LIENS STRATÉGIQUES -->
            <div>
                <!-- E-Commerce -->
                <div class="sidebar-box">
                    <h3>🛒 Star Max Shop</h3>
                    <p style="color:var(--text-muted); font-size:14px; margin-top:5px;">Achetez les t-shirts officiels, vêtements et tickets d'événements exclusifs via vos comptes locaux.</p>
                    <a href="{{ monetization.links.shop_url }}" target="_blank" class="btn-action">Visiter la Boutique (OM / MoMo)</a>
                </div>

                <!-- Cinéma Premium Payant -->
                <div class="sidebar-box" style="border-color: var(--primary);">
                    <h3>🎬 Cinéma & Séries Premium</h3>
                    <p style="color:var(--text-muted); font-size:14px; margin-top:5px;">Débloquez l'accès à notre catalogue crypté de longs-métrages africains.</p>
                    <div style="font-size: 18px; font-weight: bold; margin-top: 10px; color: var(--primary);">{{ monetization.links.cinema_price }}</div>
                    <a href="{{ monetization.links.cinema_url }}" target="_blank" class="btn-action">S'abonner via Mobile Money</a>
                </div>

                <!-- Affiliation Divertissement / Pari Foot -->
                <div class="sidebar-box" style="border-color: var(--success);">
                    <h3>⚽ Espace Pronostics & Divertissement</h3>
                    <p style="color:var(--text-muted); font-size:14px; margin-top:5px;">Consultez les analyses sportives et accédez à notre plateforme de pari partenaire locale.</p>
                    <a href="{{ monetization.links.parifoot_url }}" target="_blank" class="btn-action btn-bet">Accéder au Pari Foot</a>
                </div>
            </div>

        </div>
    </div>

    <footer style="background:#000; text-align:center; padding:40px; margin-top:40px; border-top:1px solid #222;">
        <p style="font-size:14px; color:var(--text-muted);">&copy; 2026 Star Max+ Group. L'écosystème de l'excellence panafricaine.</p>
    </footer>

    <script>
        function switchChannel(channelId) {
            const player = document.getElementById('main-player');
            const title = document.getElementById('channel-title');
            
            if(channelId.includes('http')) {
                player.src = channelId;
            } else {
                player.src = "https://www.youtube.com/embed/live_stream?channel=" + channelId;
            }
            
            event.target.parentElement.querySelectorAll('button').forEach(b => b.classList.remove('active'));
            event.target.classList.add('active');
            title.innerText = event.target.innerText;
        }

        if (window.netlifyIdentity) {
            window.netlifyIdentity.on("init", user => {
                if (!user) { window.netlifyIdentity.on("login", () => { document.location.href = "/admin/"; }); }
            });
        }
    </script>
</body>
</html>
backend:
  name: git-gateway
  branch: main

media_folder: "images/uploads"
public_folder: "/images/uploads"

i18n:
  structure: multiple_folders
  locales: [fr, en]
  default_locale: fr

collections:
  # 1. PARAMÈTRES FINANCIERS & IDENTITÉ VISUELLE
  - name: "monetization"
    label: "💰 Liens Monétisation & Revenus"
    files:
      - file: "_data/monetization.yml"
        label: "Identité, Liens & Passerelles MoMo"
        name: "links"
        fields:
          - {label: "Image du Logo Officiel (PNG/SVG transparent)", name: "logo_url", widget: "image"}
          - {label: "Lien Partenaire Pari Foot (Affiliation)", name: "parifoot_url", widget: "string", default: "#"}
          - {label: "Lien Passerelle Boutique (Paiement Mobile Money)", name: "shop_url", widget: "string", default: "#"}
          - {label: "Lien Passerelle Abonnement Cinéma", name: "cinema_url", widget: "string", default: "#"}
          - {label: "Prix de l'abonnement mensuel (Texte)", name: "cinema_price", widget: "string", default: "1 000 FCFA / mois"}

  # 2. BANDE PASSANTE DÉFILANTE (Flash Infos / Annonces Entreprises)
  - name: "ticker"
    label: "📣 Bande Défilante (Flash Info & Pubs)"
    files:
      - file: "_data/ticker.yml"
        label: "Textes de la bande passante"
        name: "news"
        fields:
          - {label: "Flash Info 1 (Urgent / Actu)", name: "line1", widget: "string", default: "Bienvenue sur Star Max+ ! La Super-App du divertissement panafricain."}
          - {label: "Annonce / Pub Entreprise 2", name: "line2", widget: "string", default: "Espace publicitaire disponible. Boostez vos ventes ici !"}
          - {label: "Flash Info / Alerte 3", name: "line3", widget: "string", default: "Suivez nos 20 chaînes TV et Radio en direct 24h/24."}

  # 3. RÉGIE PUBLICITAIRE (Bannières d'images)
  - name: "ads"
    label: "📢 Régie Pub (Bannières)"
    folder: "_ads"
    create: true
    fields:
      - {label: "Nom de l'Annonceur", name: "title", widget: "string"}
      - {label: "Affiche Publicitaire (Image)", name: "image", widget: "image"}
      - {label: "Lien de redirection (WhatsApp ou Site de l'entreprise)", name: "ad_url", widget: "string"}

  # 4. RÉGIE DES 20 CHAÎNES (Flux Live TV & Radio)
  - name: "live_channels"
    label: "📡 Configuration des 20 Chaînes"
    folder: "_channels"
    create: true
    fields:
      - {label: "Nom de la Chaîne", name: "title", widget: "select", options: ["Star Max TV", "Star Max FM", "Star Max News FM", "Star Max Info", "Star Max Action", "Star Max Cinema", "Star Max Sport", "Star Max Wild", "Star Max Music", "Star Max Life", "Star Max Media", "Star Max Prime", "Star Max International", "Star Max Celebrities", "Star Max Entertainment", "Star Max Auto", "Star Max Channel", "Star Max Discover"]}
      - {label: "Type de Flux", name: "type", widget: "select", options: ["Télévision (Vidéo)", "Radio (Audio)"]}
      - {label: "Lien du Flux Streaming (YouTube Live, Facebook Live ou M3U8)", name: "stream_url", widget: "string"}

  # 5. CATALOGUE VOD (Cinéma / Séries / Replays)
  - name: "videos"
    label: "📺 Vidéos & Replays (Par Thématique)"
    folder: "_videos"
    create: true
    i18n: true
    fields:
      - {label: "Titre de la Vidéo", name: "title", widget: "string", i18n: true}
      - {label: "Secteur / Thématique", name: "category", widget: "select", options: ["Cinéma", "Sport", "Musique", "Action", "Wild/Nature", "Auto", "Divertissement"]}
      - {label: "Miniature d'image (Couverture)", name: "thumbnail", widget: "image"}
      - {label: "Lien de la Vidéo", name: "video_url", widget: "string"}
      - {label: "Description", name: "body", widget: "markdown", i18n: true}
      - {label: "Contenu Premium (Payant par Mobile Money) ?", name: "premium", widget: "boolean", default: false}

  # 6. FIL D'ACTUALITÉS
  - name: "articles"
    label: "📰 Articles & Actualités (Bilingue)"
    folder: "_articles"
    create: true
    i18n: true
    fields:
      - {label: "Titre de l'article", name: "title", widget: "string", i18n: true}
      - {label: "Date", name: "date", widget: "datetime"}
      - {label: "Image d'illustration", name: "image", widget: "image"}
      - {label: "Catégorie", name: "category", widget: "select", options: ["Général", "Politique", "Sport", "Musique", "Célébrités"]}
      - {label: "Corps de l'article", name: "body", widget: "markdown", i18n: true}
      - {label: "Nom du Journaliste", name: "author", widget: "string"}
      - <!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Panneau d'Administration - Star Max+ Group</title>
    <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
</head>
<body>
    <script src="https://unpkg.com/decap-cms@^3.0.0/dist/decap-cms.js"></script>
</body>
</html>
