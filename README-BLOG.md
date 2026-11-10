# Editing the blog

The portfolio homepage remains ordinary HTML. Jekyll renders `blog.html` and
Markdown files in `_posts/` using `_layouts/post.html` and the existing CSS.

Connect Pages CMS to this repository and the intended editing branch after the
migration has been reviewed. The Blog posts collection exposes only `_posts/`.
Create a post, fill in the title, publication date, category, excerpt, featured
image and alt text, and write the Markdown body in the rich-text editor.
Uploads are stored in `assets/images/blog/`; their public URLs start with
`/assets/images/blog/`, including images inserted in the body.

New posts start with `published: false`. Save to keep a draft; set Published to
true only when ready to release it through the repository's publishing workflow.
Jekyll defaults unspecified posts to unpublished as an additional safeguard.
The public listing also explicitly filters for `published: true`.
Draft source files and uploaded images remain visible in a public GitHub
repository even when Jekyll excludes the draft pages from the website.

The existing article retains its explicit permalink, date, image credit and
metadata. Its food-cost comparison is `_includes/food-cost-comparison.html`,
selected by the protected `comparison: food-cost` front matter. It is outside
the editable body, so normal article editing cannot remove its markup.
Keep the existing post filename and permalink stable. Existing custom heading
IDs use Kramdown heading attributes, such as `{#income}`; confirm these survive
a Pages CMS edit/save round trip before using the editor on the live article.
The hidden metadata fields must also survive that test. Image credit is an
optional extra editor field; no credit is invented for future uploads.

## Review before deployment

Ruby, Bundler and Jekyll are not installed in this workspace. A static Python
HTTP server cannot process Liquid or build posts. On an approved environment
with compatible Jekyll dependencies, run `bundle exec jekyll build` and
`bundle exec jekyll serve`. No Gemfile or dependencies have been installed here;
choose and pin the build dependencies to match the actual GitHub Pages build
workflow before running those commands.

Check `/blog.html` and `/blog/northern-saskatchewan-food-security.html`, the
homepage, mobile navigation, image uploads, heading anchors, citations, CBC
credit, comparison, metadata and JSON-LD. Test a CMS save with both published
and unpublished posts. A normal production build must generate neither a draft
article nor a draft listing entry. Use `--unpublished` only for private local
draft previews, never for production. Do not use `--future` in production.

Confirm GitHub Pages runs Jekyll on the publishing source rather than uploading
raw source files. Pages CMS saves repository changes; whether that triggers
publication depends on the configured branch and deployment workflow. Review
on a development branch before changing the live publishing source.
