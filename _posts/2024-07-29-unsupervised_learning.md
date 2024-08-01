---
title:  "Exploring Unsupervised Learning for Complex Datasets"
mathjax: true
layout: post
categories: 
  = github
  - website
---

In this project, I delved into the realm of unsupervised learning, **applying various clustering and dimensionality reduction techniques** to two intriguing datasets: **NASA Near-Earth Objects (NEO) and Wine Quality. **This exploration aimed to simplify and interpret these complex datasets, enhancing data visualization, reducing computational costs, and improving model efficiency.

For clustering, I employed K-Means and Gaussian Mixture Models (GMM). K-Means, with its simple iterative process, performed efficiently but struggled with non-spherical cluster shapes and varying densities. In contrast, GMM, utilizing the Expectation-Maximization algorithm, captured more complex structures but required greater computational resources.

On the dimensionality reduction front, I tested Principal Component Analysis (PCA), Independent Component Analysis (ICA), and Random Projection (RP). PCA stood out by preserving overall variance and aiding visualization, while ICA excelled at separating underlying factors but was sensitive to Gaussian noise. RP, though faster, did not maintain data structure as precisely as PCA or ICA, yet proved adequate for neural network training.

My findings reinforced the no-free-lunch theorem, highlighting that the effectiveness of these methods is dataset-dependent. K-Means and GMM showed varied performance based on data characteristics, while PCA consistently reduced dimensionality with high variance retention. ICA required more components to preserve structure, especially for the NASA dataset, and RP offered speed at the cost of precision.

Integrating clustering labels with dimensionality reduction generally enhanced model performance. Notably, PCA combined with K-Means struck the best balance between bias and variance, improving neural network performance on reduced datasets. Despite PCA and ICA's higher training times, prediction times remained stable, underscoring the significance of these techniques during training.

Overall, this study confirmed PCA, particularly when paired with K-Means clustering, as a reliable method for balancing bias-variance trade-offs, ultimately boosting model generalization and performance on complex datasets.


**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/unsupervised_learning.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "8ef44ce133c04e8fa474ad6c78747b08", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/unsupervised_learning.pdf"}},
			metaData:{fileName: "unsupervised_learning.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>
