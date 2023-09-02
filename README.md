# Wav2Lip LipSync Enhancement and Parameter Tuning Guide

This README provides step-by-step instructions for enhancing LipSync using the Wav2Lip tool and introduces some tips and tricks to achieve the best results through parameter tuning. We have transitioned from the previous LipGAN model to the more advanced Wav2Lip model for improved lip synchronization.

## Step 1: Setup Wav2Lip

In this step, we will set up the necessary dependencies and download the pretrained Wav2Lip model.

1. **Install Dependencies and Libraries:**

   Run the following commands to set up the environment:

   ```python
   !rm -rf /content/sample_data
   !mkdir /content/sample_data

   !git clone https://github.com/zabique/Wav2Lip

   # Download the pretrained Wav2Lip model
   !wget 'https://iiitaphyd-my.sharepoint.com/personal/radrabha_m_research_iiit_ac_in/_layouts/15/download.aspx?share=EdjI7bZlgApMqsVoEUUXpLsBxqXbn5z8VTmoxp55YNDcIA' -O '/content/Wav2Lip/checkpoints/wav2lip_gan.pth'
   ```

2. **Install Required Python Packages:**

   Install the necessary Python packages with the following command:

   ```python
   !cd Wav2Lip && pip install -r requirements.txt
   ```

3. **Download the Pretrained Model for Face Detection:**

   Download the face detection model:

   ```python
   !wget "https://www.adrianbulat.com/downloads/python-fan/s3fd-619a316812.pth" -O "/content/Wav2Lip/face_detection/detection/sfd/s3fd.pth"
   ```

4. **Install Additional Libraries:**

   Install additional libraries for video processing and audio handling:

   ```python
   !pip install -q youtube-dl
   !pip install ffmpeg-python
   !pip install librosa==0.9.1
   ```

5. **Prepare Code for Recording Audio (Optional):**

   If needed, you can use the provided code to record audio directly within the Colab environment.

6. **Clear the Output:**

   Clear the output to proceed to the next step:

   ```python
   from IPython.display import clear_output
   clear_output()
   print("\nSetup is done.")
   ```

## Step 2: Select Video

In this step, you can choose to upload a video from your local drive or Google Drive. Follow the instructions provided to select your video:

- If uploading from your local drive, click the "Upload" button and select your video file.
- If you have a video on Google Drive, select the "Custom Path" option and provide the full path to your video.

The selected video will be displayed for your reference.

## Step 3: Select Audio

In this step, you can choose to record audio, upload audio from your local drive, or select audio from Google Drive. Follow the instructions provided to select your audio:

- If recording audio, select the "Record" option, and an audio recording will be generated.
- If uploading audio from your local drive, click the "Upload" button and select your audio file.
- If you have audio on Google Drive, select the "Custom Path" option and provide the full path to your audio.

The selected audio will be displayed for your reference.

## Step 4: Start Crunching and Preview Output

In this step, you have the opportunity to enhance LipSync results by tweaking some parameters. Here are some tips and tricks to make your LipSync even better:

- **Padding**: Adjust the `pad_top`, `pad_bottom`, `pad_left`, and `pad_right` parameters to control the padding around the video frame. Fine-tuning these values can help improve lip synchronization.

- **Rescale Factor**: The `rescaleFactor` parameter can be adjusted to resize the video. You can experiment with different values to find the optimal resolution for synchronization.

- **Smoothing**: By default, smoothing is applied to the lip movement. If you want a more raw and unedited lip movement, you can set the `nosmooth` parameter to `True`.

Here's an example command to run the Wav2Lip synchronization process with some of these parameters:

```python
# Example with padding values and rescale factor
!cd Wav2Lip && python inference.py --checkpoint_path checkpoints/wav2lip_gan.pth --face "../sample_data/input_vid.mp4" --audio "../sample_data/input_audio.wav" --pads pad_bottom pad_right --resize_factor $rescaleFactor
```

or with no smoothing:

```python
# Example with padding values, rescale factor, and no smoothing
!cd Wav2Lip && python inference.py --checkpoint_path checkpoints/wav2lip_gan.pth --face "../sample_data/input_vid.mp4" --audio "../sample_data/input_audio.wav" --pads pad_bottom pad_right --resize_factor $rescaleFactor --nosmooth
```

After the synchronization process is complete, a preview of the final video will be displayed, and you can download it from the provided link.

**Note**:
- Ensure that the selected video is not longer than 60 seconds.
- The tool may resize the video to 720p if the original resolution is higher.

Enjoy using Wav2Lip for LipSyncing and experimenting with parameter tuning to achieve the best results for your videos!
