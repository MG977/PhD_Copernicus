.. include:: html_lat.txt


.. _Map-validation:

Map validation
===============

Precision or accuracy?
````````````````````````
Precision and accuracy are often used as synonyms. **But they are not!**

- **Precision** refers to the degree to which repeated attempts (under unchanged conditions) *are close to each other*, independent of their true value. Thus, a precise quantity might be completely wrong because biased!,
- **Accuracy** refers to the degree to which repeated attempts (under unchanged conditions) *are close to the true value.* **Thus, an accurate attempt is precise and not biased.**

Let’s see how precision and accuracy work. Assume that two archers are participating in a tournament.

The first archer always hit the same spot. He is **precise**. |br|
However, his arrows are systematically displaced from the target’s centre (:numref:`Fig1_validation`). Thus, the second archer is **inaccurate**.

.. _Fig1_validation:
.. figure:: /Figure/Fig1_validation.png
	:scale: 30%
	:align: center

	The first archer's shots.

The second archer fires all his arrows grouped in the target’s centre (:numref:`Fig3_validation`). |br|
The archer is precise and unbiased. Thus, the first archer is **accurate**.

.. _Fig3_validation:
.. figure:: /Figure/Fig3_validation.png
	:scale: 30%
	:align: center

	The second archer's shots.

.. hint:: For a land cover map:

	- **Accuracy** refers to the degree to which *the information on the map* matches the real world, |br|
	- **Precision** refers to how exactly is *the data used to create the map*. This is also related to its spatial resolution, spectral characteristics, or time of acquisition (see :ref:`Fundamentals-of-remote-sensing-and-Earth-observation`).

|br|

How much is accurate a map?
````````````````````````````
Referring to the mapping process, **accuracy** is the most used performance metric and tells *“how many sites are mapped correctly.”*

Map accuracy is estimated using the **confusion matrix**, a table that relates the actual land cover of some KNOWN reference locations, called the *testing samples*, with their predicted values in the map. |br|

:numref:`Fig1_confmatrix` shows an example of a confusion matrix computed for a 4-class thematic map. In this table:

- Columns represent the instances of testing samples in the actual land cover class,
- Rows represent the instances of testing samples in the predicted land cover class,
- Instances belonging to the main diagonal (green cells) are the number of testing samples classified correctly.

.. _Fig1_confmatrix:
.. figure:: /Figure/Fig1_confmatrix.png
	:align: center

	Confusion matrix. Number of testing samples correctly classified.

:numref:`Fig2_confmatrix` highlights the number of misclassified testing samples (red cells). |br|
Overall, the confusion matrix has **434 testing samples.**

.. _Fig2_confmatrix:
.. figure:: /Figure/Fig2_confmatrix.png
	:align: center

	Confusion matrix. Number of misclassified testing samples.

.. note:: **What are the testing samples?** |br|

	To evaluate the map’s accuracy, we must compare predicted land cover classes with actual land cover classes. This is done using the testing samples, which are image pixels randomly collected, but those actual land cover is KNOWN. Results are then extended from the testing samples to the full map.

	**GUIDELINE: testing samples must be randomly collected for ALL land cover classes. There should be no less than 50 testing samples for each land cover class.**

|br|

**a. Overall accuracy** |br|
Suppose we want to quantify the proportion of correct predictions, without giving any insight into the single accuracy of land cover classes. *In other words, how many testing samples are globally labelled correctly in the classified map?* |br|
It is called **overall accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Overall\ accuracy=\frac{number\ of\ testing\ samples\ correctly\ classified}{total\ number\ of\ testing\ sample}
	:label: eqacc1

In the example of :numref:`Fig1_confmatrix` we have:

.. math:: Overall\ accuracy=\frac{65+81+85+90}{434}=74.0 \%
	:label: eqacc2

.. note:: The overall accuracy is the primary indicator used to evaluate maps.

|br|

**b. Producer’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the real-world land cover class. *In other words, for a given land cover class in the real world, how many testing samples are labelled correctly in the classified map?* |br|
This is the accuracy from the point of view of the mapmaker (the producer). It is called **producer’s accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Producer\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ column\ i}
	:label: eqacc3

In the example of :numref:`Fig1_confmatrix` we have:

.. math:: Producer\prime s\ accuracy\ for\ class\ A=\frac{65}{65+6+0+4}=86.7 \%
	:label: eqacc4

.. math:: Producer\prime s\ accuracy\ for\ class\ B=\frac{81}{4+81+11+7}=78.6 \%
	:label: eqacc5

.. math:: Producer\prime s\ accuracy\ for\ class\ C=\frac{85}{22+5+85+3}=73.9 \%
	:label: eqacc6

.. math:: Producer\prime s\ accuracy\ for\ class\ D=\frac{90}{24+8+19+90}=63.8 \%
	:label: eqacc7

Thus, the classifier is mapping real world class A with higher accuracy.

.. note:: The producer's accuracy is an indicator of how well the actual land cover information is mapped.

|br|

**c. User’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the mapped classes. *In other words, for a given class in the map, how many testing samples are really present on the ground?* |br|
This is the accuracy from the point of view of the map user. It called is called **user’s accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: User\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ row\ i}
	:label: eqacc8

In the example of :numref:`Fig1_confmatrix` we have:

.. math:: User\prime s\ accuracy\ for\ class\ A=\frac{65}{65+4+22+24}=56.5 \%
	:label: eqacc9

.. math:: User\prime s\ accuracy\ for\ class\ B=\frac{81}{6+81+5+8}=81.0 \%
	:label: eqacc10

.. math:: User\prime s\ accuracy\ for\ class\ C=\frac{85}{0+11+85+19}=73.9 \%
	:label: eqacc11

.. math:: User\prime s\ accuracy\ for\ class\ D=\frac{90}{4+7+3+90}=86.5 \%
	:label: eqacc12

Thus, the classifier is predicting the map’s class A with lower accuracy.

Typically, user’s and producer’s accuracy for a given land cover class are different. In the example of :numref:`Fig1_confmatrix`, 86.7% of the testing samples for real-world class A are correctly identified as class A in the map (producer’s accuracy). However, only 56.5% of the areas identified as class A in the map are actually being class A on the ground.

.. note:: The user's accuracy is an indicator of how well the map describes the actual land covers.

|br|

.. hint:: **Small activity** |br|
	Which is the accuracy of your map? |br|
	Calculate the overall accuracy and the per-class producer’s accuracy and user’s accuracy of your own map. Try the free `Confusion matrix online calculator <http://www.marcovanetti.com/pages/cfmatrix/>`_.

|br|

.. seealso:: For additional information, see the practical guide on `Map Accuracy Assessment and Area Estimation <http://www.fao.org/3/i5601e/i5601e.pdf>`_ of `FAO <http://www.fao.org/home/en/>`_.

|br|
|br|

(v.2103211230)