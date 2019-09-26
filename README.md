# Multiple Object Forecasting

The repo contains the Citywalks dataset and code for the paper: 

**Multiple Object Forecasting: Predicting Future Object Locations in Diverse Environments. WACV 2020 (to appear).**

Content available:

- The Citywalks dataset
- Raw tracking labels
- Ground truth trajectory labels
- Metadata
- STED trajectory predictions
- Evaluation code

Content coming soon:

- STED model code
- Results on MOT-17

Citywalks contains a total of 501 20-second video clips of which 358 contain at least one valid pedestrian trajectory.  

<p align="center"> 
<img src="citywalks.gif">
</p>


# Downloading Citywalks videos
The raw videos can be downloaded here: [[Google Drive](https://drive.google.com/open?id=1oMN-fsWvEjUZ9Ah_3JwUuIY7cmR0OP_Q)] 
[[One Drive](https://1drv.ms/u/s!AlCsPcYF4WdzjGVQzrAPeteUH4rS?e=tET0GY)]

To download from the terminal:
```bash
pip install gdown
gdown https://drive.google.com/uc?id==1oMN-fsWvEjUZ9Ah_3JwUuIY7cmR0OP_Q
```
OR 
```bash
wget -O citywalks.zip "https://onedrive.live.com/download?cid=7367E105C63DAC50&resid=7367E105C63DAC50%211637&authkey=AJmkgXYpBLsX-CM"
```

# Downloading tracking results

We use Yolov3 and Mask-RCNN to detect pedestrians, and DeepSORT to track pedestrians. Tracking results can be downloaded here: [[Google Drive](https://drive.google.com/open?id=12-_FiphR5m0Yd455pem13OVnvCvi-yIn)] [[One Drive](https://onedrive.live.com/?authkey=%21AJvssSoCKvoJ2ew&cid=7367E105C63DAC50&id=7367E105C63DAC50%211635&parId=root&action=locate)]

To download from the terminal:
```bash
gdown https://drive.google.com/uc?id=12-_FiphR5m0Yd455pem13OVnvCvi-yIn
```
OR 
```bash
wget -O tracks.zip "https://onedrive.live.com/download?cid=7367E105C63DAC50&resid=7367E105C63DAC50%211635&authkey=AOlVtKFP76Rhn90"
```

The files are organized as follows:

- vid: Name of video clip
- filename: City of original recording
- frame_num: Frame number. 30FPS.
- track: Track ID assigned by DeepSORT
- cx: Center x bounding box coordinate
- cy: Center y bounding box coordinate
- w: Bounding box width
- h: Bounding box height
- track_length: Current length (in frames) of this track
- labelled: 1 if this frame is labelled, 0 otherwise. For a track to be labelled, it must follow at least 29 previous tracked frames and have at least 60 following tracked frames. i.e. the pedestrian must have been tracked continuously for at least 3 seconds.
- requires_features: 1 if this frame requires features, 0 otherwise. All labelled frames and the previous 29 frames require features. This is the motion history used for MOF.

# Downloading metadata

Weather and time of day metadata is also avaiable [[Google Drive](https://drive.google.com/open?id=163VmkvnB_ruTDUTezsz1jxBJtdoH98Vc)] [[One Drive](https://1drv.ms/u/s!AlCsPcYF4WdzjGacBbIcCK9Xxsda?e=ty0LlL)]

To download from the terminal:
```bash
gdown https://drive.google.com/uc?id=163VmkvnB_ruTDUTezsz1jxBJtdoH98Vc
```
OR 
```bash
wget -O outputs.zip "https://onedrive.live.com/download?cid=7367E105C63DAC50&resid=7367E105C63DAC50%211638&authkey=ALMIImBBNMMCP88"
```

The file is organized as follows:
- city: City of original recording
- time: Time of day (day or night). 'night' is defined as the point at which street lights turn on
- weather: Weather conditions of recording (sun, overcast, snow, or rain)
- first_clip: First clip for this city that is labelled with this metadata (inclusive)
- last_clip: Last clip for this city that is labelled with this metadata (inclusive)


# Evaluating Multiple Object Forecasting models

We use ADE, FDE, AIOU, and FIOU metrics to evaluate Multiple Object Forecasting models on Citywalks. The ground truth trajectories and predictions from STED can be downloaded here: [[Google Drive](https://drive.google.com/open?id=1KZ08pzp1j8P598VNIMR3vSeFcnf3871d)] [[One Drive](https://1drv.ms/u/s!AlCsPcYF4WdzjGTxFjuPdOkhb-4p?e=3nylt1)]

To download from the terminal:
```bash
gdown https://drive.google.com/uc?id=1KZ08pzp1j8P598VNIMR3vSeFcnf3871d
```
OR 
```bash
wget -O outputs.zip "https://onedrive.live.com/download?cid=7367E105C63DAC50&resid=7367E105C63DAC50%211636&authkey=AFNJWoXVjzfuNVI"
```

These predictions can then be evaluated using the file ```evaluate_outputs.py```. Example usage:

```bash
python evaluate_outputs.py -gt ./outputs/ground_truth/ -pred ./outputs/sted/
``` 

If run correctly, the result should be equal to Table 2 in our paper.

The files are organized as follows:
- vid: Name of video clip
- filename: City of original recording
- frame_num: Frame number. 30FPS.
- x1_t: Left bounding box coordinate at t timesteps in the future
- y1_t: Top bounding box coordinate at t timesteps in the future
- x2_t: Right bounding box coordinate at t timesteps in the future
- y2_t: Bottom bounding box coordinate at t timesteps in the future


Please open an issue if you have any questions.

# Acknowledgements
We would also like to thank Daniel Sczepansky for collecting the videos used in the Citywalks dataset. Full videos are available at: https://www.youtube.com/poptravelorg
