# Personal Site

## To Do

- [x] define separate tailwind files, one for markdown/blog posts, one for everything else
- [x] setup mythic beasts rpi
- [x] install docker on rpi
- [x] send image to rpi
- [x] run image on rpi
- [x] preview site from mbp
- [ ] hook up running image to domain

## About

- Static site, created with Hugo
- Styled with Tailwind
- Containerized with Docker
- Served with nginx
- Running on a Raspberry Pi 3

## Create new blog post

`hugo new content/posts/<post_name>.md`

## Development Mode

### Process 1

- `hugo server &`

### Process 2

- `cd themes/ashwin`
- `./tw-dev.sh`

## Production Build

- use `./tw-prod.sh` instead

## Docker Build

- [documentation](https://hugomods.com/docs/docker/)

```sh
docker build -t ashwinsundar .
```

## Docker Run

```sh
docker run -p 1313:80 ashwinsundar
```
## Deployment

### Local

- `docker image build -t ashwinsundar/ashwinsundar .`
- `docker image push ashwinsundar/ashwinsundar`

### Server

- `docker image pull ashwinsundar/ashwinsundar`
- `docker container stop <id>`
- `docker container run -p 1313:80 ashwinsundar/ashwinsundar`

## Server Setup

### General Information

- Hardware: Raspberry Pi 3
- OS: Ubuntu 18.04.6
- additional installations:
  - nginx
  - docker (follow [these instructions](https://docs.docker.com/engine/install/ubuntu/))
  - lynx (helpful for debugging web hosting issues)
  - ranger (optional, TUI file browser)


### Step 1: Run server in Docker container

#### Locally:

- `docker build -t ashwinsundar .`
- `docker tag ashwinsundar {registry_name}/ashwinsundar` - allows docker push to push to image registry
- `docker image push {registry_name}/ashwinsundar` - the last arg will be referred to as `{image_name}`

#### Server:

- `docker login` (if using Docker Registry)
  - get access token from registry site
  - instructions may vary if a different image registry is used
- `docker image pull {image_name}` 
- `docker image run -p 1313:80 {image_name}`
- `lynx localhost:1313` - confirm that website is running locally

### Step 2: Configure nginx

#### Server:

- create a file `/etc/nginx/sites-available/ashwinsundar`
- replace `server_name` arguments with the actual site/IP that server can be reached at, and receive requests on port 80

```nginx
  # /etc/nginx/sites-available/ashwinsundar
  server {
      listen 80;
      listen [::]:80;
      server_name ashsun1.hostedpi.com www.ashsun1.hostedpi.com;

      location / {
          proxy_pass http://localhost:1313;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
      }
  }
```

- create symbolic link `sudo ln -s /etc/nginx/sites-available/ashwinsundar /etc/nginx/sites-enabled/`

#### Locally:

- Browse to `{server_name}`. Site should be running!

#### Additional Info:

- `listen 80` and `listen [::]:80` map IPv4 and IPv6 requests, respectively
- `proxy_pass` says where to redirect all listeners at `80`. `1313` is the port that we mapped earlier to the Docker container's port `80` (which is also running it's own nginx service inside)

### Step 3: Connect to domain

Replace {server_name} with {domain}?


## Code tree

```shell
├── assets
├── content
│   └── posts # markdown posts for blog. create new post with `hugo new content posts/{title}.md`
├── data # data objects, accessible from templates with
│   └── projects.json # independent projects that I've worked on, accessible from templates with `site.Data.projects
├── hugo.toml # hugo config
├── layouts
│   |── 404.html # 404 page layout
│   └── home.html # homepage layout
├── public # site pages. auto-generated by `hugo server`
├── readme.md
├── resources
├── static
└── themes
    └── ashwin
        |── archetypes
        |   |── default.md # front matter for blog posts created with `hugo new content` (https://gohugo.io/content-management/archetypes/)
        |   └── posts.md # front matter for blog posts created with `hugo new content posts/`
        |── assets
        |   └── css
        |       |── main.tw.css # tailwind css setup for all pages except posts/ 
        |       |── posts.tw.css # tailwind css setup for posts/
        |       |── o.main.tw.css # main tailwind output, auto-generated by ./tw.dev.sh
        |       └── o.posts.tw.css # tailwind output for posts/, auto-generated by ./tw.dev.sh
        ├── layouts
        |   |── _default
        |   |   |── baseof.html # base template for all pages (https://gohugo.io/templates/base/#define-the-base-template)
        |   |   |── list.html # renders lists (https://gohugo.io/templates/lists/)
        |   |   └── single.html # base template for single pages. Hugo renders all markdown files using this template (https://gohugo.io/templates/single-page-templates/)
        |   └── partials
        |   |   |── footer.html
        |   |   |── header.html
        |   |   |── main_css.html # snippet for retrieving o.main.tw.css. used by main_head.html
        |   |   |── main_head.html # head content for all pages except posts/. Used by baseof.html
        |   |   |── menu.html # renders a menu
        |   |   |── posts.css.html # snippet for retrieving o.posts.tw.css. used by posts_head.html
        |   |   |── posts_head.html # head content for posts/. used by single.html
        |   |   └── terms.html # terms of service. can probably remove
        ├── static
        ├── tailwind.config.js # tailwind configuration
        ├── tw-dev.sh # tailwind dev mode
        └── tw-prod.sh # tailwind production script
```
