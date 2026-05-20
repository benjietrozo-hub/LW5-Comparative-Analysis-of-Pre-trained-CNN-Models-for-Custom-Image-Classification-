# LW5-Comparative-Analysis-of-Pre-trained-CNN-Models-for-Custom-Image-Classification-

collab file: https://colab.research.google.com/drive/1q38-iqwdL9_L_8DRHUOX9GGG0lv7WoFD?usp=sharing

keras files: https://drive.google.com/drive/folders/1OkxJxkeEHq9X74h-v67tWiSeXRdxHhyw?usp=sharing

A. Model Performance
1. Which pre-trained model achieved the highest accuracy? Why?

Among the pre-trained models, EfficientNetB0 achieved the highest accuracy at 87.91%. It performed better because its architecture balances depth, width, and image resolution, allowing it to capture important leaf details like texture, veins, and shape more effectively. It also used the correct preprocessing method, which helped improve its performance.

2. Which model had the lowest performance? What could be the reason?

ResNet50 had the lowest accuracy at 62.27%. One reason is that the model is much larger and more complex compared to the dataset size. Since the dataset only had a limited number of images per class, the model could not fully learn the differences between the Ficus species within 20 epochs. This caused underfitting, meaning the model did not learn enough patterns from the data.

3. How did loss values compare across models at the final epoch?

EfficientNetB0 had the lowest validation loss (0.4137), which matches its high accuracy. MobileNetV2 followed with 0.4793, while ResNet50 had the highest loss (1.5191), showing that it struggled to learn the dataset properly. Overall, lower loss values were associated with better model performance.

B. Evaluation Metrics
4. Why is accuracy not enough to evaluate a model?

Accuracy alone is not enough because the dataset is imbalanced. Some classes had many more images than others. A model may achieve high accuracy by predicting the larger classes correctly while still performing poorly on smaller classes. Metrics like F1-score and ROC-AUC provide a fairer evaluation because they measure how well the model performs across all classes.

5. Which model had the best F1-score? What does it indicate?

The Lab4_Model achieved the best macro F1-score at 0.90, followed closely by EfficientNetB0 at 0.883. A high F1-score means the model balanced both precision and recall well across all classes. This indicates that the model performed consistently, even on difficult Ficus species.

6. How did Precision and Recall differ across models?

Most models showed higher precision than recall on difficult classes. This means the models were careful when making predictions — they only predicted certain classes when confident, but they also missed many correct samples. For example, some species were identified correctly when predicted, but many actual images of those species were not detected.

C. Confusion Matrix Analysis
7. Which classes were frequently misclassified?

The most difficult classes across the models were:

Florida_Strangler_Fig
Short-Leaf_Fig
Port_Jackson_Fig
Council_Tree

These species likely share similar leaf shapes, colors, and textures, making them harder to distinguish.

8. What patterns did you observe in the confusion matrix?

Some classes such as Creeping_Fig and Indian_Banyan were classified almost perfectly because they have unique visual features. On the other hand, difficult classes were often confused with each other. This suggests that those species have overlapping visual characteristics, making classification more challenging.

D. ROC and AUC
9. Which model had the highest AUC score?

EfficientNetB0 achieved the highest AUC score at 0.9920, followed closely by MobileNetV2 and Lab4_Model. This indicates that EfficientNetB0 was very effective at distinguishing the correct class from incorrect ones.

10. What does AUC tell us about model performance?

AUC measures how well the model ranks the correct class higher than the wrong classes across different thresholds. A high AUC means the model is very good at separating classes, even if some final predictions are still incorrect. It is especially useful for imbalanced datasets.

E. Explainability (Grad-CAM)
11. What did Grad-CAM reveal about model decision-making?

Grad-CAM showed which parts of the image the models focused on during prediction. EfficientNetB0 and MobileNetV2 mainly focused on the leaf area, including the veins and edges, while ResNet50 showed less focused attention, which matches its lower performance.

12. Did the model focus on relevant image regions?

Yes. The better-performing models focused on important botanical features such as leaf shape, vein patterns, and margins. For difficult classes, the heatmaps were more scattered, showing that the models had trouble finding clear distinguishing features.

13. Which model produced the most meaningful heatmaps?

EfficientNetB0 produced the most focused and meaningful Grad-CAM heatmaps. Its ability to capture details at multiple scales helped it focus on the most important regions of the leaf.

F. Model Comparison & Improvement
14. Which model would you recommend for deployment? Why?

EfficientNetB0 is the best model for deployment because it achieved the best balance between accuracy, reliability, and model size. It had the highest AUC score and strong overall performance while remaining lightweight enough for practical applications like mobile or web deployment.

15. How can you further improve your best-performing model?

Some ways to improve the model are:

Collect more images for difficult classes
Apply deeper fine-tuning with lower learning rates
Use test-time augmentation (TTA)
Apply label smoothing to improve generalization

These improvements could help increase accuracy beyond 90%.

G. Real-World Application
16. How can your model be applied in real-world scenarios?

The model can be used in several real-world applications, such as:

Mobile apps for plant identification
Urban tree inventory systems
Biodiversity and environmental research
Invasive species monitoring

It can help users quickly identify Ficus species using leaf images.

17. What are the risks of deploying an inaccurate model?

Incorrect predictions may lead to wrong species identification, which can affect ecological research and invasive species monitoring. Since the model is not 100% accurate, predictions with low confidence should still be reviewed by experts.

18. How can this system be integrated into a mobile/web app?

For mobile apps, the model can be converted into TensorFlow Lite (TFLite) format and used offline in Android or iOS applications.

For web apps, the model can be deployed using frameworks like FastAPI, where users upload images and receive predictions with confidence scores and Grad-CAM visualizations.

The system should display:

Predicted species name
Confidence score
Top-3 predictions
Grad-CAM heatmap for explainability
