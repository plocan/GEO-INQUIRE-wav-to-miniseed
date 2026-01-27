## GEO-INQUIRE Audio Processing Tool

Convert WAV audio recordings to FLAC (with EMSO metadata) and MiniSEED/StationXML (FDSN-compliant). Includes a GUI for managing metadata from TXT or JSON files.

Developed by PLOCAN (Plataforma Oceánica de Canarias) as part of the GEO-INQUIRE project.

### What it does
- WAV → FLAC (lossless compression) with EMSO metadata embedded
- WAV → MiniSEED (for seismic/acoustic data workflows)
- Generates FDSN-compliant StationXML for each recording
- GUI for EMSO + StationXML metadata entry (supports TXT/JSON templates)
- Automatic start/end time extraction from filename with UTC offset support

### Inputs
- WAV files (single file or folder batch processing)
- EMSO metadata: upload TXT/JSON template or enter manually in the GUI
- StationXML metadata: upload TXT/JSON template or enter manually in the GUI

### Outputs
- `.flac` - FLAC audio with EMSO metadata tags
- `.mseed` - MiniSEED (FDSN standard)
- `.station.xml` - StationXML (FDSN standard)

### Quick start

#### Option A: Using Conda (Recommended for Mac/Linux)
```bash
# Create environment from file
conda env create -f environment.yml

# Activate environment
conda activate geoinquire

# Launch Jupyter
jupyter lab
```

#### Option B: Using pip
1. Install Python 3.9+
2. Install requirements:
   ```bash
   pip install -r requirements.txt
   ```
3. Open `20260104_GEO-INQUIRE_wav_flac_miniseed_V12.ipynb` in Jupyter
4. Run the main code cell to launch the GUI
5. Select WAV files and load your metadata templates
6. Click **Start Processing**

#### Option C: Google Colab (No Installation)
1. Go to [Google Colab](https://colab.research.google.com/)
2. Upload the notebook file
3. Run the installation cell, then the main code

### Mac Users
If you're on macOS (especially Apple Silicon M1/M2/M3), see **[README_Mac_Installation.md](README_Mac_Installation.md)** for detailed instructions and troubleshooting.

### Metadata templates
Included example templates (customize for your deployment):
- `EMSO_PLOCAN_metadata.json` / `.txt` - EMSO metadata for FLAC files
- `PLOCAN metadata for XML files.json` / `.txt` - StationXML metadata

### Example files
The `examples/` folder contains sample output files:
- `channelA_2020-06-27_01-40-14.flac` - FLAC with EMSO metadata
- `channelA_2020-06-27_01-40-14.mseed` - MiniSEED output
- `channelA_2020-06-27_01-40-14.station.xml` - StationXML output

Use these to verify the expected output format. Test the tool with your own WAV files.

### QC Viewer
A separate notebook (`MiniSEED_QC_Viewer.ipynb`) is provided for quality control:
- Validate StationXML against FDSN schema (uses IRIS validator)
- Compute PPSD (Probabilistic Power Spectral Density) with instrument response correction
- Generate ASD (Amplitude Spectral Density) plots
- Designed for quick spot-checks of a few files (not for batch processing entire datasets)

### Technical notes
- EMSO required fields are validated in the GUI
- Start/end times are extracted from filenames (format: `name_YYYY-MM-DD_HH-MM-SS.wav`)
- Output sample rate is controlled by `FINAL_SAMPLING_RATE` in the notebook
- StationXML metadata can be loaded from TXT or JSON files
- This tool assumes no digitizer decimation in the field; decimation is applied in post-processing. If your digitizer already decimates, adjust the `datalogger_input_sample_rate` and decimation settings accordingly
- StationXML is written by ObsPy, then post-processed to enforce strict FDSN schema order (e.g., `Source` before `Sender`, ordered decimation fields)

### Standards compliance
- **MiniSEED**: FDSN standard format for seismic/acoustic time series data
- **StationXML**: FDSN standard format for station metadata and instrument response
- **EMSO**: European Multidisciplinary Seafloor and water column Observatory metadata conventions

### License
[Add your license here]

### Acknowledgments
This tool was developed as part of the GEO-INQUIRE project at PLOCAN.
