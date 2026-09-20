FROM docker.io/squidfunk/mkdocs-material:9.5.34

# nodejs/npm for cspell; the rest are WeasyPrint's native dependencies, needed by
# the pdf-export plugin (libgobject, pango and friends are not in the base image).
RUN apk add --no-cache --update \
      nodejs npm \
      glib pango gdk-pixbuf fontconfig ttf-dejavu

WORKDIR /site
COPY ./package*.json /site/
COPY ./requirements.txt /site/

# Dependencies
RUN npm ci && pip install -r requirements.txt
ENTRYPOINT ["/usr/local/bin/mkdocs",  "serve",  "--dirtyreload",  "-a", "0.0.0.0:8000"]
