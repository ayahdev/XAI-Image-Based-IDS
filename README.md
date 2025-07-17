# XAI-Image-Based-IDS

This GitHub repository contains the code used in the research work titled: Towards understanding the behavior of image-based network intrusion detection systems.

Code explanation:

Step 1: Generate grey-scale images.

*_1_session_to_image.ipynb_* --- The code in this notebook references https://github.com/davidyslu/USTC-TK2016/blob/master/3_Session2Png.py. It takes the session in the .pcap format and converts it to 32x32 grey-scale images. Set the file paths in the block titled "Converting Pcap Sessions to Images". Set the ethernet version in the *ethernet_version* list as such; to keep the Ethernet layer, set the list to [1,0,0]. To replace the Ethernet layer with 0s, set it to [0,1,0]. To completely remove the Ethernet layer, set it to [0,0,1].

Step 2: Train a CNN model on the 32x32 grey-scale images.

Step 3: Generate heatmaps using the trained model.

*_3_gradcam_heatmap_generation.ipynb_* --- This notebook is used to generate heatmaps using the greyscale images and the trained model. Set the paths in the block titled "Loading Model and Settings Paths".

Step 4: Applying the reverse lookup technique.

*_4_reverse_lookup_single_file.ipynb_* --- This notebook contains the various functions used to perform a reverse lookup on the heatmaps and understand the highly impacting bytes to the model's decisions. The default color of the highly impacting bytes set in the file is Yellow based on the Viridis color scale. 

To use this notebook:
1. Set the paths in the block titled "Loading Model and Setting Paths".
2. Set the grey-scale image size (should be the image size of the heatmaps as well).
3. Set the path for tshark.exe (default path already set).
4. Set the _has_ethernet_ variable according to the Ethernet version from Step 1. If you are keeping the Ethernet layer, or replacing it with 0s, then set the variable to True. Else, set it to False.
5. If the model trained is a binary classification model, then set the _binary_classification_ variable to True. Else, set it to False.
6. If using the Viridis scale, then keep the color values in the block titled "Defining Functions" in the _binary_mask_generation_ function the same. However, if you would like to perform the reverse lookup on bytes of different importance, hence, have a different color, change the variables _lower_yellow_threshold_ and _upper_yellow_threshold_ accordingly.
7. In block "Doing Reverse Lookup for Session", adjust the _index_of_name_in_path_ according to the path of the grey-scale image that was set in the block "Loading Model and Setting Paths". This is the make sure that all the files generated from this notebook have the correct file name. For instance, if the path for the grey-scale session image is as follows: "C:\\Desktop\\Folder_1\\session_1.png", then the _index_of_name_in_path_ should be set to 3 ( start count from 0, and split on \\ ).

Thank you for checking this work, and kindly cite our work at __.
