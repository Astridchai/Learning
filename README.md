# Learning

MS- AI900 certificate learning notes

==================
Learning materials
Trainings: https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-fundamentals/?practice-assessment-type=certification

Lesson 1 Beginning
LLM & SLM
LLM: large language models (LLMs). Powerful, more variables, most cost on training and use.
SLM: Small language models. More focused on specific topic areas, and usually cost less.

Common uses of generative AI include:
1.	Implementing chatbots and AI agents that assist human users.
2.	Creating new documents or other content (often as a starting point for further iterative development)
3.	Automated translation of text between languages.
4.	Summarizing or explaining complex documents.

Computer vision (accomplished by using large numbers of images to train a model)
1.	Image classification. A form of computer vision. It trained with images that are labeled with the main subject of the image (in other words, what it's an image of) so that it can analyze unlabeled images and predict the most appropriate label - identifying the subject of the image.
   ![image](https://github.com/user-attachments/assets/893e806f-9f99-412b-a290-4470968e5a9d)

2.	Object detection. A form of computer vision. It trained the module to identify the location of specific objects in an image. It provides bounding boxes around the detected objects and labels them with a category (e.g., "car," "dog," "person"). It does not care about the exact pixel-level details of the object. For instance, it will tell you that there’s a car in the image, but it won’t tell you which pixels belong to the car.
![image](https://github.com/user-attachments/assets/77818d19-b325-48c4-9bc8-2c787760c9fc)

3.	Semantic segmentation. An advanced form of computer vision. The model can identify the individual pixels in the image that belong to a particular object. . It assigns a class label to every pixel in an image, effectively dividing the image into meaningful regions based on the objects or features present. E.g. In the same image, semantic segmentation would color all the pixels corresponding to the car as "car," and the pixels corresponding to the road as "road," providing a detailed mask of the scene.
   
Example of Use Cases:
•	Object Detection: Self-driving cars need to detect specific objects (cars, pedestrians, traffic signs) to navigate safely.
•	Semantic Segmentation: Medical imaging (e.g., identifying tumors or organs) requires pixel-level accuracy, which is achieved through semantic segmentation.

