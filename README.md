
# **COVID-19 US Confirmed Cases Time-Series Visualization**

This project generates an engaging animated GIF that visualizes the progression of confirmed COVID-19 cases across US counties over time. Leveraging public health data and geospatial libraries, it provides a dynamic view of the pandemic's spread.

## **Overview**

The script automates the process of fetching time-series COVID-19 data, merging it with US county geographical boundaries, generating individual map frames, and compiling these frames into an animated GIF. It's designed for efficiency, utilizing parallel processing to speed up frame generation.

## **Features**

* **Animated Time Series:** Visualizes the spread of COVID-19 confirmed cases across US counties over chosen time intervals.
* **County-Level Granularity:** Provides detailed insights by displaying data at the county level.
* **Optimized Performance:**
    * **Parallel Processing:** Utilizes `joblib` to generate map frames concurrently across multiple CPU cores, significantly speeding up the visualization process.
    * **In-Memory Frame Generation:** Avoids repetitive disk I/O by generating and processing image data in memory before GIF compilation.
* **Customizable Output:** Easily adjust animation speed (frames per second), image resolution (DPI), and the time interval between frames.
* **Dark Mode Aesthetic Capabilities:** Configure with a black background for a modern and distinct visual style.
* **Automated Cleanup:** Deletes temporary image files after the GIF is created to conserve storage.

## **How It Works**

The visualization is created through the following steps:

1.  **Data Loading:** Confirmed COVID-19 cases time-series data is loaded from the Johns Hopkins University CSSE GitHub repository.
2.  **Map Data Preparation:** US county boundary shapefile data is loaded and preprocessed using `geopandas`.
3.  **Frame Generation (Parallel):**
    * For each selected date (e.g., every 3rd or 30th day), the script extracts relevant case data.
    * This data is merged with the geographical county information.
    * A choropleth map is then generated, colored based on the number of confirmed cases, with a black background.
    * The generated map is captured directly into memory as an image array.
    * This process runs in parallel for all selected dates.
4.  **GIF Compilation:** All in-memory image arrays are collected and assembled into a single animated GIF using `imageio`.
5.  **Display & Cleanup:** The final GIF is displayed directly in the execution environment (e.g., Google Colab), and all intermediate frame data is automatically deleted.

## **Setup and Installation**

### **Recommended: Google Colaboratory**

This project is ideally suited for Google Colab, as it provides a free environment with pre-installed libraries and sufficient computing resources for most runs.

1.  **Upload Shapefile:** Upload the US county shapefile (`cb_2018_us_county_500k.shp`) to your Colab session (e.g., into the `/content/sample_data/` folder, or adjust the path in the code).
2.  **Run Cells:** Simply paste the provided Python code into a Colab notebook cell and run it.

### **Local Environment**

If you prefer to run the project locally, ensure you have Python 3.7+ installed along with the following libraries. It's often recommended to use a virtual environment.

1.  **Download Shapefile:** Download the `cb_2018_us_county_500k.shp` file (and its accompanying `.dbf`, `.shx`, `.prj`, etc., files) from the [US Census Bureau website](https://www2.census.gov/geo/tiger/GENZ2018/shp/cb_2018_us_county_500k.zip) and place them in your project directory.
2.  **Install Dependencies:**
    ```bash
    pip install pandas geopandas matplotlib mapclassify imageio joblib numpy
    ```
    *(Note: `geopandas` can sometimes be complex to install locally due to its geospatial dependencies. Using `conda` or referring to the [Geopandas installation guide](https://geopandas.org/en/stable/getting_started/install.html) might be helpful if you encounter issues.)*
3.  **Run Script:** Execute your Python script from your terminal:
    ```bash
    python your_script_name.py
    ```

## **Usage**

1.  **Execute the Code:** Run all the cells in your Google Colab notebook or execute the Python script.
2.  **Monitor Progress:** The script will print messages to the console indicating which frame it's processing.
3.  **View Output:**
    * Upon completion, the animated GIF (`covid_animation.gif`) will be displayed directly within your notebook's output cell.
    * The GIF file will also be saved to the main directory of your Colab session (or your script's directory if running locally), allowing you to download or share it.

## **Customization Options**

You can easily modify the animation's behavior and appearance by adjusting parameters in the code:

* **Frame Interval (`dates_to_process`):**
    * Located in the `Merging Data Set With US Map` section.
    * Change `dates_to_process = all_date_columns[::30]` to:
        * `::1` for every single day (slowest, most frames).
        * `::7` for every week.
        * `::14` for every two weeks.
        * A larger number results in fewer frames and a faster overall process.
* **Animation Speed (FPS):**
    * Located in the `Animation Output` section.
    * Modify `fps=1` in `imageio.get_writer(...)`.
    * `fps=10` makes the animation play 10 frames per second (faster).
    * `fps=1` makes it play 1 frame per second (slower, default for this code).
* **Image Quality/Resolution (DPI):**
    * Located within the `generate_single_frame` function.
    * Adjust `dpi=50` in `plt.savefig(..., dpi=50, ...)`.
    * Lower DPI (e.g., `30`) means faster processing and smaller GIF size, but lower image quality.
    * Higher DPI (e.g., `100`) means better quality but slower processing and larger GIF size.
* **Map Size (`figsize`):**
    * Located within the `generate_single_frame` function.
    * Modify `figsize=(12, 7)` in `plt.subplots(...)` to change the width and height of each map image.
* **Number of Parallel Workers (`n_jobs`):**
    * Located in the `Merging Data Set With US Map` section (in the `Parallel` call).
    * `n_jobs=-1` (default) uses all available CPU cores, recommended for maximum speed.
    * You can set a specific number (e.g., `n_jobs=4`) if you want to limit worker count.
* **Background Color:**
    * Located within the `generate_single_frame` function.
    * The current code sets the background to black (`facecolor='black'` and `ax.set_facecolor('black')`) and the title color to white (`color='white'`). You can modify these values to your preferred colors.
