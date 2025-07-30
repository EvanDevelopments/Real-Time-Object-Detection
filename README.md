
# **Real-Time Traffic Congestion Detection**

This repository presents a dynamic and efficient Python-based application for real-time object detection in video streams. It leverages cutting-edge deep learning and computer vision technologies to identify and localize objects instantly, providing a powerful tool for visual analysis.

## **Overview**

This application is designed to process video footage frame by frame, utilizing a pre-trained YOLOv5 model to accurately detect various objects. The detected objects are visually highlighted with bounding boxes and displayed in real-time, offering an intuitive and dynamic representation of object presence and movement. The project focuses on delivering high performance and ease of use, making it an excellent foundation for various real-world applications.

## **Features**

* **Instantaneous Object Detection:** Achieves near real-time performance, crucial for applications requiring immediate insights from video data.
* **High-Performance Model Integration:** Seamlessly incorporates the highly optimized YOLOv5s model from Ultralytics, renowned for its balanced speed and accuracy in object detection tasks.
* **Versatile Video Input:** Supports a wide range of input sources, including pre-recorded video files (like the provided motorway CCTV example) and live camera feeds (e.g., webcams, surveillance cameras).
* **Clear Visual Output:** Utilizes OpenCV to render crisp bounding boxes and detection labels directly onto the video frames, ensuring intuitive and immediate understanding of the detected objects.
* **Pythonic & Modular Design:** Developed with clear, well-structured Python code, promoting easy understanding, maintainability, and future extensibility for custom projects.


## **How It Works**

The core functionality of this real-time object detection system is built upon a streamlined and efficient pipeline:
1. * **Model Loading:** A compact yet powerful yolov5s model is loaded directly from PyTorch Hub using torch.hub.load. This method simplifies model acquisition and ensures robust object recognition without requiring manual download of model weights.
2.* **Video Stream Capture:** The cv2.VideoCapture function from the OpenCV library is employed to open the specified video file and capture individual frames sequentially.
3.* **Real-Time Inference:** Each captured video frame is then fed into the loaded YOLOv5 model. The model performs rapid inference, identifying and classifying objects within the frame.
4.* **Result Rendering:** The detection results, which include precise bounding box coordinates, class labels (e.g., 'car', 'person'), and confidence scores, are processed. OpenCV's drawing functionalities are then used to overlay these visual indicators directly onto the original video frame.
5. * **Live Visualization:** The annotated video frames are continuously displayed in a dedicated window using cv2.imshow, providing a smooth, real-time visual feed of all detected objects. This process loops, ensuring continuous monitoring until the user decides to quit.

## **Setup and Installation**
To get this exciting project up and running on your local machine, please follow these straightforward steps:

**Prerequisites**
* **Python 3.7+:** Ensure you have a compatible Python version installed.
* **Git:** Make sure Git is installed and configured on your system for cloning repositories.

**Installation Steps**
Clone the YOLOv5 Repository:
Begin by cloning the official Ultralytics YOLOv5 repository, as our project builds upon its robust framework and dependencies.

git clone https://github.com/ultralytics/yolov5
cd yolov5

Install Dependencies:
Navigate into the newly cloned yolov5 directory. Then, install all the necessary Python packages listed in the requirements.txt file. This includes essential libraries such as torch, opencv-python, matplotlib, and numpy.

pip install -r requirements.txt

(Note: This step involves downloading PyTorch and other substantial libraries, so a stable and fast internet connection is highly recommended.)

Place Your Video File:
Ensure the video file you intend to analyze (e.g., Motorway CCTV - 4 Split - 10mins - 1280 x 720.mp4) is placed in a location easily accessible by your Python script. Remember to update the video variable within your script (your_script_name.py) with the correct, full path to your video file.

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
