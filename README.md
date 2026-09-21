<p align="center">
  <img src="images/readme-banner.jpg" alt="Mixedreams: Your dreams, my music. Israeli and world music DJ in Seattle, Bellevue and Redmond" width="100%">
</p>

# Mixedreams

Single-page website for **Mixedreams**, an Israeli and world music DJ service for weddings, bar and bat mitzvas, parties and productions in the greater Seattle area.

Live site: https://www.mixedreams.com

It is a plain static site: one HTML file with inline CSS and JavaScript, plus a folder of images. There is no build step, no framework and nothing to install.

## What's on the page

| Section | Purpose |
| --- | --- |
| Hero | "Your dreams, my music." headline with an English / Hebrew crossfader, plus the main "Plan your event" button |
| Services | Weddings and celebrations, bar and bat mitzvas, custom productions |
| Photo bands | Dance floor and Israeli music imagery |
| Gear | The equipment list, shown as a signal path from computer to speakers |
| Contact | Tap-to-call and tap-to-text phone number, and an inquiry form that emails the details |

The page is responsive (phone, tablet, laptop) and respects the "reduce motion" setting on visitors' devices.

## Project structure

```
mixedreams/
├── index.html          The whole site: content, styles and scripts
├── robots.txt          Tells search engines what to crawl and where the sitemap is
├── sitemap.xml         Lists the one page of the site for Google Search Console
├── 404.html            Friendly page shown for old or mistyped addresses
├── audio/
│   └── background.mp3      Optional background music (you add this file)
├── README.md           This file
└── images/
    ├── logo.png            Logo for the black background (used on the site)
    ├── logo-original.png   Logo in its original colours, transparent background
    ├── favicon.png         Browser tab and home-screen icon (512 x 512)
    ├── og.jpg              1200 x 630 preview image for Facebook, WhatsApp and search shares
    ├── readme-banner.jpg   Banner shown at the top of this README (not used on the website)
    ├── waveform.jpg        Hero background
    ├── crowd.jpg           Dance floor band
    ├── telaviv.jpg         Israeli music band
    ├── dj-controller.jpg   Gear section band
    └── dancers.jpg         Contact section background
```

## Running it locally

Double-click `index.html` to open it in your browser. To preview it the way a web server would serve it, run this in the project folder and open http://localhost:8000:

```
python3 -m http.server 8000
```

## Editing the site

Everything is in `index.html`. Search for the text you want to change.

| To change... | Look for... |
| --- | --- |
| Headline and intro text | `<section class="hero"` |
| Hebrew headline | `class="mix__b"` |
| Services | `<section class="services"` |
| Gear list | `<ol class="chain">` |
| Phone number | `phone__number`, the Call and Text buttons, and `"telephone"` in the JSON-LD block at the top. Update all of them together. |
| Social links | `contact__social` |
| Colours | The `:root` block at the top of the `<style>` section (`--blue`, `--pale`, `--black` and so on) |
| Page title and search description | The `<title>` and `<meta name="description">` tags in the `<head>` |

### Replacing images

Keep the same file names so nothing in the HTML needs to change. Save photos as JPEG, around 2000 to 2200 px wide, compressed to roughly 150 to 500 KB. Large originals slow the page down, especially on phones.

The logo is `images/logo.png`. It is a transparent PNG with light lettering so it stays readable on black. The tab icon is `images/favicon.png`, made from the ring mark of the logo on a black tile.

## Contact form setup

The form sends its details to email through [Web3Forms](https://web3forms.com), a free service that works with static sites.

1. Go to web3forms.com, click **Create your Form**, and enter the Gmail address that should receive inquiries.
2. Confirm the verification email. Your **access key** is then issued.
3. In `index.html`, replace `YOUR_ACCESS_KEY` in the hidden `access_key` field with your key.
4. Publish, then send yourself a test inquiry from the live site. Check Spam the first time and mark it "Not spam".

Notes:

- The access key is not a password. It is visible in the page source by design, and it keeps your email address out of the page.
- The free plan has a monthly submission limit. Check web3forms.com/pricing for the current number.
- The form includes a hidden spam trap field (`website_url`). Leave it in place.

## Deploying on GitHub Pages

GitHub Pages hosts static sites for free. On a free GitHub account the repository must be **public**.

1. Create a new repository on GitHub and upload the contents of this folder, so that `index.html` is at the top level of the repository.
2. Open the repository's **Settings**, then **Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose the `main` branch and the `/ (root)` folder, and save.
4. After a minute or two the site is live at `https://YOUR-USERNAME.github.io/REPOSITORY-NAME/`.

### Using www.mixedreams.com

1. In **Settings, Pages**, enter `www.mixedreams.com` under **Custom domain** and save. GitHub adds a `CNAME` file to the repository.
2. At your domain registrar, add these DNS records:
   - A **CNAME** record for `www` pointing to `YOUR-USERNAME.github.io`
   - If you also want `mixedreams.com` without the `www` to work, four **A** records for the apex domain pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`
3. Wait for DNS to update (usually minutes, sometimes a few hours), then tick **Enforce HTTPS** in **Settings, Pages**.

GitHub's instructions are at https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site and are the source of truth if anything above has changed.

Every time you push a change to `main`, GitHub republishes the site automatically. It can take a minute or two to appear.

## Background music

The site has an optional **Play music** button in the bottom-left corner.

- Save your track as `audio/background.mp3`. The button appears only when the file exists, so the site works normally without it.
- Music never starts by itself. Browsers block sound until the visitor taps or clicks, so the visitor starts it with the button. It fades in, loops, and pauses when they switch to another tab.
- Keep the file small (about 2 to 4 MB). GitHub Pages serves it as-is, and the page only fetches a tiny part of it until someone presses play.
- Use music you own or have a licence to play publicly. A DJ mix of other artists' songs is not automatically cleared for a public website.
- To change the volume, edit `var LEVEL = 0.5;` near the bottom of `index.html` (0 is silent, 1 is full volume).

## Search engine optimisation (SEO)

Already built into `index.html`:

- A keyword-focused page title and description, a visible "Israeli and world music DJ in Seattle" line inside the main heading, and a Questions section written around what people search for.
- Business details for search engines (JSON-LD structured data): name, phone, languages, services and the areas served.
- Social preview tags (Open Graph and Twitter) using `images/og.jpg`.
- `robots.txt`, `sitemap.xml` and a custom `404.html`.

After every content change that matters, update the date in `sitemap.xml`.

After publishing:

1. In **Google Search Console**, add the property for `https://www.mixedreams.com/`, submit `https://www.mixedreams.com/sitemap.xml`, then use **URL Inspection** on the home page and click **Request indexing**.
2. Create a **Google Business Profile** (service-area business, category "DJ service") with your phone, website link, service areas, photos and services. This is the biggest factor for local searches.
3. Keep the same business name and phone number on Facebook, SoundCloud, LinkedIn and any wedding or event directories, and link each of them back to the website.
4. Ask happy clients for Google reviews, and add real testimonials and event photos to the page when you have them.

## Troubleshooting

- **The form says "did not send".** Check that `YOUR_ACCESS_KEY` has been replaced with your real key and that you are connected to the internet.
- **An image is missing on the live site.** File names on GitHub Pages are case-sensitive. `Crowd.jpg` and `crowd.jpg` are different files, so match the names in the HTML exactly.
- **The logo shows as text.** `images/logo.png` is missing or misnamed, so the page falls back to plain text.
- **A change isn't showing.** Wait a couple of minutes for GitHub to republish, then hard-refresh the browser (Ctrl+Shift+R, or Cmd+Shift+R on a Mac).
- **Fonts look different.** The page loads Frank Ruhl Libre and Hanken Grotesk from Google Fonts. Without an internet connection it falls back to system fonts.

## Credits and licences

- Fonts: [Frank Ruhl Libre](https://fonts.google.com/specimen/Frank+Ruhl+Libre) and [Hanken Grotesk](https://fonts.google.com/specimen/Hanken+Grotesk), both from Google Fonts under the SIL Open Font License.
- Photos: stock images licensed for use on this site. Keep your licence receipts on file, and check the licence terms before reusing the images anywhere else.
- Logo and written content: © Mixedreams.

