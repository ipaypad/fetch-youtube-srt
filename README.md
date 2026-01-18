
# (claude skills) YouTube Transcript Downloader

This is an advanced transcript extraction tool built with Python and `yt-dlp`. It is designed to bypass YouTube's anti-scraping mechanisms (such as "429 Too Many Requests", Bot detection, and HLS encrypted streams) to automatically download, clean, and save transcripts as plain text files named after the video title.

## 🌟 Key Features

* **Identity Masking**: Uses `cookies.txt` to simulate a real logged-in session, solving the "Sign in to confirm you’re not a bot" issue.
* **Auto Format Conversion**: Handles complex HLS/m3u8 subtitle streams and utilizes FFmpeg to convert them into readable text.
* **Smart Text Cleaning**: Automatically strips timestamps (00:00:00), HTML tags, WEBVTT headers, and repetitive lines common in auto-generated subtitles.
* **Automated Naming**: Retrieves the video title and sanitizes illegal characters (e.g., `|`, `?`, `:`) to generate clean `.txt` files directly.

---

## 🛠️ Installation (Windows Guide)

### Step 1: Install Scoop (Package Manager)

To easily install dependencies like FFmpeg, it is recommended to use Scoop. Open **PowerShell (Run as Administrator)**:

```powershell
# Set Execution Policy
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
# Install Scoop
iwr -useb get.scoop.sh | iex

```

### Step 2: Install Environment Dependencies

Use Scoop to install Python and FFmpeg:

```powershell
scoop install python ffmpeg

```

### Step 3: Install Python Libraries

Run the following in your project terminal:

```powershell
pip install -U yt-dlp requests

```

---

## 🔑 Getting YouTube Cookies (Crucial Step)

YouTube's restrictions on automated tools (especially from cloud/datacenter IPs) are extremely strict. You must use cookies exported from your local browser:

1. Install the browser extension: **[Get cookies.txt locally](https://www.google.com/search?q=https://microsoftedge.microsoft.com/addons/detail/get-cookiestxt-locally/ccmclkhmhdadpjcobghmclnhhcheihmo)** (Available for Chrome/Edge).
2. Log in to your YouTube account.
3. Click the extension icon and select **Export**.
4. Rename the downloaded file to **`cookies.txt`** and place it in the same directory as `fetch_transcript.py`.

---

## 🚀 Usage

### 1. Extract a Single Video

Run in your terminal:

```powershell
python fetch_transcript.py "https://www.youtube.com/watch?v=vBu6zJAWcGs"

```

### 2. Network Proxy (Optional)

If you need a proxy to access YouTube, set the environment variables before running the script:

```powershell
$env:HTTP_PROXY="http://127.0.0.1:7890"  # Replace with your proxy port
$env:HTTPS_PROXY="http://127.0.0.1:7890"

```

---

## 📂 File Description

| Filename | Description |
| --- | --- |
| `fetch_transcript.py` | Main logic script containing cleaning and downloading functions. |
| `cookies.txt` | User authentication credentials (manual export required; keep private). |
| `[Video Title].txt` | **Output**: The cleaned, readable plain-text transcript. |

---

## ⚠️ Troubleshooting

* **ERROR: Sign in to confirm you’re not a bot**: This means your `cookies.txt` has expired. Refresh your YouTube page in the browser and export a new cookie file.
* **Failed to decrypt with DPAPI**: This occurs when using the `cookies_from_browser` mode with a recently updated browser. This script avoids this by using the `cookies.txt` file method.
* **Requested format is not available**: The script is configured with the `allow_unplayable_formats` parameter to ensure it grabs the metadata and subtitles even without a downloadable video stream.

---

## 📜 License

MIT License. For educational and personal research purposes only.

---

**Would you like me to create a batch-processing script that reads a list of URLs from a file and processes them all at once?**
