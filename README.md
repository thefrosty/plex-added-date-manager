# Plex Added Date Manager

App that interacts with the Plex API to modify "Recently Added" date values.

![Plex Added Date Manager](.github/recently-added-manager.png?raw=true "Plex Added Date Manager")

## Setup Instruction (Docker)

```docker
services:

  recently-added-manager:
    image: thefrosty/plex-added-date-manager:latest
    container_name: recently-added-manager
    restart: unless-stopped
    environment:
      - PLEX_BASE_URL=https://192.168.1.20:32400
      - PLEX_TOKEN=your_plex_token_here
      - PLEX_VERIFY_SSL=False
      - PLEX_MOVIE_SECTION_ID=3
      - PLEX_TV_SECTION_ID=2
      - PLEX_MUSIC_SECTION_ID=9
      - PLEX_PAGE_SIZE=20
      - PLEX_TIMEZONE=America/Los_Angeles
    ports:
      - 8501:8501
```

## Setup Instructions (local)

Run the app in a container so its Python environment stays off the host.

1. **Create your env file** from the example and fill in your Plex server:
   ```bash
   cp .env.example .env
   ```
2. **Start the app:**
   ```bash
   docker compose up --build
   ```
3. **Open** `http://localhost:8501`.

`PLEX_BASE_URL` is requested from inside the container, so it has to be an address the container can reach. For Plex on
this machine, use `http://host.docker.internal:32400`. For Plex on another machine, use that machine's address, for
example `http://192.168.1.20:32400`.

When Plex requires secure connections, its certificate is issued for a `plex.direct` name. Use that name as
`PLEX_BASE_URL`. A raw IP address fails certificate verification.

`PLEX_MOVIE_SECTION_ID`, `PLEX_TV_SECTION_ID`, and `PLEX_MUSIC_SECTION_ID` set the library selected when each tab opens.
Movie and TV default to `1` and `2`. Leave the music id blank to open the first artist library. Each tab also has a
section menu for the other libraries of that type.

`PLEX_PAGE_SIZE` is the page size selected on first load. It must be `20`, `50`, or `100`, and it defaults to `20`.

`PLEX_TIMEZONE` is an IANA timezone name, such as `America/Los_Angeles`. Added dates are shown and saved in that zone.
It defaults to `UTC`.

Stop the app with Ctrl+C, then:

```bash
docker compose down
```

## Usage

Movies, TV Series, and Music each load one page at a time. Page size is 20, 50, or 100. Sort by added date, title, or
year, and filter by year. "Title contains" narrows the items on the current page. The Music tab lists albums in an
artist library.

Select items across pages and apply one added date to the whole selection. "Lock added date" tells Plex to keep that
field. Turn images off when a page feels heavy.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
