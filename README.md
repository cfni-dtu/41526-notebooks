# 41526 notebooks

Interactive Jupyter notebooks for DTU course 41526 (Fracture Mechanics),
runnable entirely in a browser with nothing installed.

Notebooks are organised in subfolders under `notebooks/`:

```
notebooks/
  lecture03/
    ModeIII_plastic_zone.ipynb        — Mode III plastic zone
    ModeIII_singular_behaviour.ipynb  — Mode III stress singularity vs. displacement field
  lecture04/
    ModeI_plastic_zone.ipynb          — Mode I plastic zone
    Westergaard_periodic_cracks.ipynb — K_I for a periodic array of collinear cracks
```

## Run in your browser

- **Mode III plastic zone:**
  https://cfni-dtu.github.io/41526-notebooks/lab/index.html?path=lecture03/ModeIII_plastic_zone.ipynb
- **Mode III singular behaviour (stress vs. displacement):**
  https://cfni-dtu.github.io/41526-notebooks/lab/index.html?path=lecture03/ModeIII_singular_behaviour.ipynb
- **Mode I plastic zone:**
  https://cfni-dtu.github.io/41526-notebooks/lab/index.html?path=lecture04/ModeI_plastic_zone.ipynb
- **Periodic array of collinear cracks (Westergaard):**
  https://cfni-dtu.github.io/41526-notebooks/lab/index.html?path=lecture04/Westergaard_periodic_cracks.ipynb

This runs via [JupyterLite](https://jupyterlite.readthedocs.io/): each
notebook executes client-side in the browser (WebAssembly/Pyodide), so
there's no server, no account, and nothing to install. The first run
installs `sympy` on the fly (a few seconds); after that everything runs
locally in the tab.

### Seeing an old version of a notebook?

The first time you open one of these links, JupyterLite copies the
notebook into your browser's own local storage and treats that as your
personal workspace from then on — like a real Jupyter server preserving
your edits. That means if we update a notebook later, your browser may
keep showing you the old copy it already saved, instead of fetching the
new one.

To get the current version:
- Open the link in a **private/incognito window**, or
- **Clear the site's stored data**: in Chrome/Edge, open DevTools (F12) →
  Application tab → "Clear site data" while on the page (or go to the
  site settings for `cfni-dtu.github.io` and clear cookies/site data
  there).

## For the lecturer: how this is built

Every push to `main` triggers `.github/workflows/deploy.yml`, which builds
the JupyterLite site from `notebooks/` (preserving the `lectureNN/`
subfolder structure) and publishes it to GitHub Pages.

If you update a notebook students have already opened, mention the
"Seeing an old version?" note above — their browser will otherwise keep
showing the version it cached on first visit.

To add a notebook to an existing lecture, just drop a new `.ipynb` into
that `lectureNN/` folder and push — no other changes needed. To add a new
lecture number, create `notebooks/lectureNN/` with its notebook(s) inside
and push — the workflow picks up any folder under `notebooks/`
automatically.

To test a build locally first:

```
python3 -m venv .venv
source .venv/bin/activate
pip install jupyterlite-core jupyterlite-pyodide-kernel jupyter_server
jupyter lite build --contents notebooks --output-dir _output
jupyter lite serve --output-dir _output
```
