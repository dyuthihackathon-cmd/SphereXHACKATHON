# SphereX — Multi-Wavelength Time-Domain Astronomy Explorer

**Explore the universe across multiple wavelengths and observation times using real astronomical archive data.**

SphereX is a scientific web application designed to explore astronomical observations, spectral information, time-domain variability, source catalogues, image comparisons, and moving-object candidates.

The application connects to public astronomical archives and services, including NASA SPHEREx, WISE/NEOWISE, ESA Gaia DR3, ZTF DR24, NASA JPL Horizons, and the Minor Planet Center.

## Project Features

### 1. Sky Explorer
- Interactive astronomical sky viewer.
- HiPS survey layers, including AllWISE, SPHEREx, 2MASS, DSS2, and SDSS.
- RA/DEC coordinate navigation.
- Sky-coordinate and pixel-coordinate conversion.

### 2. Observations Explorer
- Search astronomical observations using sky coordinates.
- Explore SPHEREx, WISE, AllWISE, NEOWISE, and ZTF image coverage.
- FITS image preview and inspection.
- FITS cutout export.

### 3. Spectral Explorer
- SPHEREx DR1 102-channel all-sky spectral cube.
- Spectral extraction using sky coordinates.
- Wavelength and channel exploration.
- Exposure-depth and quality-flag information.
- Handles intentionally blank channels 51 and 52.

### 4. Time-Domain Research
- NEOWISE-R W1 and W2 light curves.
- ZTF DR24 optical light curves.
- Multi-epoch observation comparison.
- Light-curve quality filtering.

### 5. Image Comparison
- Side-by-side image comparison.
- Split-screen comparison.
- Epoch blinking.
- WCS-aligned difference imaging.
- FITS difference-image export.

### 6. Sources and Astrometry
- Gaia DR3 source search.
- Pan-STARRS DR2 catalogue access.
- 2MASS source catalogue access.
- Proper-motion propagation using Astropy.

### 7. Moving Objects and Ephemerides
- Source detection and candidate tracklet analysis.
- NASA JPL Horizons ephemeris queries.
- Minor Planet Center cross-verification.
- Candidate classifications with uncertainty and human-review status.

### 8. Research and Export
- Research session ledger.
- CSV and JSON exports.
- Markdown research reports.
- Archive connectivity checks and provenance information.

---

# Installation and Setup

## Requirements

Install these before running SphereX:

| Software | Requirement |
|---|---|
| Node.js | 20.19+ or 22.12+ |
| Python | 3.11 or newer |
| npm | Included with Node.js |
| Git | Optional |

Check your installations:

```powershell
node --version
npm --version
python --version
```

## Run SphereX on Windows

The following instructions use Windows PowerShell.

### Step 1 — Extract the project ZIP

Extract the downloaded project ZIP into a folder on your computer.

Open PowerShell in the extracted project root directory.

The root directory must contain:

```text
package.json
server.ts
vite.config.ts
README.md
backend/
src/
```

### Step 2 — Create the Python virtual environment

Run:

```powershell
python -m venv backend\.venv
```

Activate it:

```powershell
.\backend\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Then activate again:

```powershell
.\backend\.venv\Scripts\Activate.ps1
```

### Step 3 — Install Python backend dependencies

Run:

```powershell
python -m pip install --upgrade pip
```

Then:

```powershell
pip install -r backend\requirements.txt
```

This installs FastAPI, Uvicorn, Astropy, Astroquery, NumPy, SciPy, PyArrow, Photutils, Reproject, PyVO, and other backend dependencies.

### Step 4 — Install frontend dependencies

Make sure you are in the project root directory.

Run:

```powershell
npm install
```

Wait until installation finishes successfully.

### Step 5 — Start SphereX

Run:

```powershell
npm run dev
```

This is the recommended startup method.

The application server will:
- Start the Python FastAPI backend.
- Start the frontend through Vite.
- Forward `/api` requests to the backend.
- Serve the application on port 3000.

Open:

**http://localhost:3000**

Keep the PowerShell window open while using SphereX.

---

# Alternative: Run Frontend and Backend Separately

Use this method if you prefer two terminal windows or need to troubleshoot the backend independently.

### Terminal 1 — Backend

From the project root:

```powershell
cd backend
..\backend\.venv\Scripts\python.exe -m uvicorn main:app --host 127.0.0.1 --port 8000 --reload
```

Backend health endpoint:

```text
http://127.0.0.1:8000/api/health
```

Backend interactive API documentation:

```text
http://127.0.0.1:8000/docs
```

### Terminal 2 — Frontend

Open another PowerShell window in the project root and run:

```powershell
npm run dev:vite
```

Open:

**http://localhost:5173**

Keep both terminal windows running.

---

# Verify the Application

### Check backend health

Open:

```text
http://127.0.0.1:8000/api/health
```

A successful response should contain:

```json
{
  "status": "ok",
  "service": "SphereX Scientific FastAPI Bridge",
  "version": "1.0.0"
}
```

### Check archive connectivity

Open:

```text
http://127.0.0.1:8000/api/archive/status
```

This checks the connectivity of configured external archive services.

A configured service does not necessarily mean that its archive is currently reachable.

### Run frontend tests

From the project root:

```powershell
npm test
```

### Run TypeScript checks

```powershell
npm run lint
```

### Create a production frontend build

```powershell
npm run build
```

The generated frontend files are placed in the `dist` directory.

### Run backend tests

```powershell
.\backend\.venv\Scripts\python.exe -m pytest -v backend\tests
```

---

# Official Scientific Data Sources

SphereX is configured to access the following public astronomical services:

| Dataset / Service | Provider |
|---|---|
| SPHEREx DR1 | NASA / IPAC IRSA |
| WISE / AllWISE | NASA / IPAC IRSA |
| NEOWISE-R | NASA / IPAC IRSA |
| Gaia DR3 | European Space Agency |
| ZTF DR24 | Caltech / IPAC |
| Pan-STARRS DR2 | STScI MAST |
| 2MASS | NASA / IPAC IRSA |
| JPL Horizons | NASA JPL |
| Minor Planet Center | IAU |
| SIMBAD | CDS Strasbourg |

Official documentation:

- SPHEREx: https://irsa.ipac.caltech.edu/spherex-archive-documentation/
- WISE: https://irsa.ipac.caltech.edu/Missions/wise.html
- Gaia: https://gea.esac.esa.int/archive/
- ZTF: https://irsa.ipac.caltech.edu/data/ZTF/docs/
- Pan-STARRS: https://catalogs.mast.stsci.edu/
- JPL Horizons: https://ssd.jpl.nasa.gov/horizons/

For detailed data access and scientific methodology, see:

- `docs/DATA_GUIDE.md`
- `docs/SCIENTIFIC_METHODOLOGY.md`
- `docs/API.md`

---

# Troubleshooting

### Error: Python module not found

Activate the virtual environment and reinstall dependencies:

```powershell
.\backend\.venv\Scripts\Activate.ps1
pip install -r backend\requirements.txt
```

### Error: npm cannot find package.json

You are probably in the wrong directory.

Navigate to the extracted project root, where `package.json` exists.

### Error: Port already in use

Stop the existing SphereX process before starting another instance. The default ports are:

- Frontend unified server: `3000`
- FastAPI backend: `8000`
- Vite development server: `5173`

### Error: 502 or 503 from an archive

This can indicate an external archive timeout, an unavailable provider, or a backend request failure.

Check:

```text
http://127.0.0.1:8000/api/archive/status
```

External archive availability and network connectivity are not guaranteed.

### Error: PowerShell script execution is blocked

Run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Then activate the virtual environment again.

---

# Scientific Integrity

SphereX is designed to distinguish retrieved astronomical measurements from unavailable or invalid data.

- External archive failures should be reported rather than replaced with fabricated observations.
- Blank SPHEREx DR1 channels 51 and 52 are handled explicitly.
- Missing variance information is not invented.
- Moving-object candidates are not automatically classified as confirmed discoveries.
- Catalogue coverage limitations and data-quality flags should be considered when interpreting results.

# Project Information

**Project:** SphereX  
**Category:** Astronomy / Space Science / Scientific Data Exploration  
**Frontend:** React, TypeScript, Vite  
**Backend:** Python, FastAPI  
**Scientific Libraries:** Astropy, Astroquery, NumPy, SciPy, Photutils, Reproject, PyArrow

**Repository:**  
https://github.com/dyuthihackathon-cmd/SphereXHACKATHON

**NASA Space Apps Challenge Project**

