# 🤓 I Tried Implementing KNN From Scratch—Here’s What I Learned

So I’ve been messing around with machine learning lately, and one algorithm that kept popping up was K-Nearest Neighbors (KNN). It sounded simple enough—“just find the closest neighbors”—but I wanted to *actually* understand what that meant.

Instead of just running `sklearn` and calling it a day, I built my own KNN classifier from scratch. Along the way, I played with toy datasets, tuned hyperparameters, and even added some cool visuals (including a GIF!) to really get what KNN is doing.

Here’s how it went.

---

## 🧠 What Even *Is* KNN?

KNN is basically pattern recognition using a ruler.

- You give it labeled data (like blue dots and red dots).
- You get a new data point.
- It finds the **k** closest points from the training set.
- It lets those neighbors vote on what the new point should be.

It doesn’t “train” a model in the traditional sense—it just memorizes the data and looks around when it needs to make a decision.

---

## 🧪 Step 1: Testing on Toy Datasets

To get started, I used three classic toy datasets:

1. **Linearly separable** – Two classes split cleanly.  
2. **Moons** – Two moon-shaped clusters.  
3. **Circles** – Concentric circular classes.

These are perfect for visualizing how decision boundaries form.

![Toy Datasets Scatter Plot](/Users/zwehtetaung/Desktop/Project%20BAPE/Medium/KNN/images/Toy%20Datasets.png)  
*Three toy datasets: linearly separable, moons, and circles. Each one challenges KNN differently.*

---

## ⚙️ Step 2: Using `scikit-learn` KNN

To get a baseline, I ran `KNeighborsClassifier` from `scikit-learn` on all three datasets using the same `k`.

```python
from sklearn.neighbors import KNeighborsClassifier

model = KNeighborsClassifier(n_neighbors=5)
model.fit(X_train, y_train)
preds = model.predict(X_test)
```

![KNN Visual.png](/Users/zwehtetaung/Desktop/Project%20BAPE/Medium/KNN/images/KNN%20Visual.png)

*KNN with the same `k` applied to all three datasets. Notice how it performs well on linearly separable data, struggles a bit on moons, and totally breaks down on circles.*

Even with the same setup, performance changes based on the shape of the data. That was my first "aha" moment—**geometry matters**.

---

## ⚒️ Step 3: Building KNN From Scratch

Then I wrote my own KNN class in Python using just NumPy. No external libraries, no black-box functions. Here’s the basic flow:

- **Distance:** Used Euclidean distance to compare points.

- **Sorting:** Grabbed the k closest training points.

- **Voting:** Found the most common class.

- **Prediction:** Assigned the class to the test point.

It was surprisingly straightforward—and kind of satisfying.

---

## 🎨 Step 4: Visualizing the Neighbors

Here’s where it got fun: I added a visualization method to my custom KNN class.

It does two things:

1. Plots the training points and test point.

2. Draws **dashed lines** from the test point to its k nearest neighbors.

This made KNN *click* for me.

![KNN Visual with different k.png](/Users/zwehtetaung/Desktop/Project%20BAPE/Medium/KNN/images/KNN%20Visual%20with%20different%20k.png)

*On the circles dataset, changing `k` shifts the decision. Small `k` captures the local structure. Larger `k` starts blending the classes.*

You can literally watch how the choice of `k` affects the prediction.

---

## 📈 Bonus: Accuracy vs. `k`

To dig a little deeper, I plotted accuracy as `k` increases.

*As `k` increases, accuracy first improves, then drops. Too low = overfitting. Too high = oversmoothing.*

<img src="file:///Users/zwehtetaung/Desktop/Project%20BAPE/Medium/KNN/images/Accuracy.png" title="" alt="Accuracy.png" width="449">

There’s a sweet spot where the model balances local detail with general trends.

---

I also made a GIF that animates how predictions evolve as `k` increases. You can literally *see* the model becoming more biased toward the majority class.

*As `k` increases, the model gets smoother—and more biased toward the dominant class. Small clusters get ignored.*

<img title="" src="file:///Users/zwehtetaung/Desktop/Project%20BAPE/Medium/KNN/images/KNN.gif" alt="KNN.gif" width="502">

This one really helped me understand why tuning `k` matters. It's not just about performance—it's about *what kind of mistakes* the model makes.

---

## 💡 Final Thoughts

Here’s what I took away from building KNN by hand:

- KNN is simple on the surface, but full of nuance.

- Visualization is a cheat code for understanding.

- Implementing from scratch beats any tutorial.

- Tuning `k` changes the model’s entire personality.

If you’re starting out in ML, try building a classic algorithm from scratch—even a simple one like KNN. You’ll learn way more than you expect.

📎 *Code and notebook are [here]*  
🎯 *Let me know if you want to dive deeper or try a new algorithm next!*
