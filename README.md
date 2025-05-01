<!-- $ bundle exec jekyll serve -->

# Offline Install Instructions

Please Extract the folder and then run the following command 

It will automatically download necessary packages and opening the link the web page can be viewed

```
$ docker run -it --rm -v "$PWD":/usr/src/app -p "4000:4000" starefossen/github-pages
```

# Using HTML and CSS for Personal Branding on GitHub Pages

GitHub Pages is a free and effective platform to showcase your skills, portfolio, and personal identity as a developer. By using HTML and CSS, we can build a personalized website that reflects your brand.

## Example: [hassin23ayz.github.io](https://hassin23ayz.github.io/)

This personal site demonstrates a clean and minimal design powered by HTML and CSS, highlighting projects, personal information, and links. This is the same page as the zipped offline version

## Design Tips

A strong layout makes the site easy to navigate and visually balanced. in this project a particula layout is followed
for example on the right the browsing related options are put and at bottom different social media links 

- **semantic HTML** like `<header>`, `<section>`, `<article>`, and `<footer>` for meaningful structure.
- **CSS Grid** are great tools for responsive and flexible layouts.
- **consistent fonts** and pairing them carefully (e.g., one for headings, one for body).
- Applied **spacing (padding and margin)** to avoid a cluttered look.
- Kept it **accessible**: high contrast, readable fonts, and no flashing animations.
- Added subtle **transitions** to create a smooth user experience.
- Kept styles **modular and organized**—use classes and group similar rules such as posts in a folder
