Introduction To Differential Privacy
====================================


Introduction
============

The era we are living in is data-driven; more data is being generated now than ever before. Much of this data is being used to improve our lives - be it recommending the best videos to watch after a tiring day at work, suggesting the best gifts to buy when it's our best friend's birthday, or keeping our birthday party photos sorted so that we can cherish them years later. Many large companies are using data to gain insights into their financial and operational activities. Machine Learning (ML) has made our life easier in many ways ... but is it just about improving the quality of our lives?  

This raises a more fundamental question: can machine learning change the way we live?  Can it positively impact our health and happiness?  The answer is both "Yes" and  "No."

Machine learning and data
=========================

Machine Learning is both data-driven and research-driven.  In general, the richer and more numerous the data, the better the research on that particular topic will be.  All data cannot, however, be released for research; many types of data include non-public personal or business information, and the redistribution of such information is typically restricted by laws, rules, contracts, and ethical standards.

Take, for example, building machine learning models to solve medical problems like radiology diagnosis.  Better, faster diagnoses could result in improved outcomes for patients facing a wide range of medical issues.  In order to train these models, researchers need medical health records, like patient case histories (e.g., ICD/CPT codes) and the corresponding radiology images for each patient (e.g., DICOM-format CT scans).

In many countries and legal jurisdictions, these records are considered to be protected health information (PHI).  Storing, sharing, and even processing PHI is often highly restricted.  Even without the existence of such laws and rules, no one would want their identifiable medical records shared without permission on the Internet or in public otherwise.  But without access to such information, how can researchers train models to help these patients?  


As we can see, real-world legal and ethical issues often prevent researchers from helping solving real-world problems.  Without data, neither traditional statistical analysis nor predictive machine learning applications can be developed.  Are we stuck in a world without a solution?

Luckily, the answer is no.  Differential privacy is an approach to solving exactly this problem. In the words of Andrew Trask, OpenMined's Founder, "Differential Privacy is the process to answer questions or solve problems using the data that we cannot see."  In this way, researchers from all over the world can use private data in their research work without identifying the individual.

.. figure:: https://user-images.githubusercontent.com/19529592/91377299-b58fbf80-e83c-11ea-9b56-a068ea3155c6.png
    :alt: my-picture1
    :align: center
    :figclass: align-center

    (Privacy Preserving AI (Andrew Trask) | MIT Deep Learning Series )

Why is Differential Privacy so important ?
==========================================

The aim of any privacy algorithm is to keep one's private information safe and secured from improper or undesired use. Differential privacy aims to keep an individual's identity secured even if their data is being used in research.  A different approach to privacy is “Data Anonymization,” which typically involves removing information from a dataset that can allow for re-identification of records.  In cases where records correspond to individuals, this normally means removing personally-identifiable information (PII). However, there are issues with this approach:

* Anonymizing certain fields may make the entire dataset useless and unfit for any analysis.

* Motivated actors can use other sources of information, such as public records or information available on the "dark web," to re-identify individuals or organizations in "anonymized" datasets.

* If the dataset is large or will be used frequently or by many, it can be difficult to model the types of queries that will be made and how risks might emerge.  This makes many useful datasets prone to misuse.

Hence, traditional anonymization processes have known weaknesses and are increasingly considered to be fundamentally incorrect approaches.  One of the most well-known examples of attack involves Netflix, which previously held an annual recommendation engine challenge.  Between 2006 and 2009, Netflix released an anonymized data of over 100 million movies from almost half a million users.  They used traditional anonymization techniques to remove PII from these records, believing that this data could not be re-identified.


.. figure:: https://user-images.githubusercontent.com/19529592/91381064-14a50280-e844-11ea-9dd0-1af088c3924d.png
    :alt: netflix
    :align: center
    :figclass: align-center

    Image Credits: Secure and Private AI (Udacity)

Unfortunately, two researchers at the University of Texas were able to successfully re-identify some users. They released a `paper <https://www.cs.utexas.edu/~shmat/shmat_oak08netflix.pdf>`_ , detailing their methodology and the results.  In this paper, they explain how they were able to combine information from IMDB with the Netflix Prize data.  Ten years down the line they have published yet another `research paper <https://www.cs.princeton.edu/~arvindn/publications/de-anonymization-retrospective.pdf>`_  where they have reviewed de-anonymization of datasets in the present world. There are other instances too where such attacks have been made which led to the leakage of private information.

.. figure:: https://user-images.githubusercontent.com/19529592/91381399-ef64c400-e844-11ea-8535-0180f37962de.png
    :alt: research
    :align: center
    :figclass: align-center

Now that we understand why traditional anonymization techniques need improvement and why Differential Privacy is so important, let's learn more about how Differential Privacy is actually implemented.


How is Differential Privacy implemented ?
=========================================

According to `Cynthia Dwork <https://www.microsoft.com/en-us/research/people/dwork>`_- *“Differential privacy” describes a promise, made by a data holder, or curator, to a data subject: “You will not be affected, adversely or otherwise, by allowing your data to be used in any study or analysis, no matter what other studies, data sets, or information sources, are available.”*

Thus this new area of research addresses the paradox of learning nothing about an individual while learning useful information about the population. This is done by sending queries (a function applied to a database) to the data curator (a protocol run by the set of individuals, using the various techniques for secure multiparty protocols). The goal of the curator is to answer all the queries with highest possible accuracy without leaking any individual information using various Differential-Privacy algorithms.

These algorithms add random noise to the queries and to the database. This is done in two ways:

* Local Differential Privacy
* Global Differential Privacy

Local Differential Privacy
--------------------------

In local differential privacy the random noise is applied at the start of the process(local) level i.e when the data is sent to the data curator/aggregator. If the data is too confidential, generally the data generators do not want to trust the curator and hence add noise to the dataset beforehand. This is adopted when the Data Curator cannot be completely trusted.

.. figure:: https://user-images.githubusercontent.com/19529592/91381482-1e7b3580-e845-11ea-9419-cd6bdbbd9dbf.png
    :alt: local
    :align: center
    :figclass: align-center

    Image Credit: Google Images

Global Differential Privacy
---------------------------
In Global differential privacy the random noise is applied at the global level i.e when the answer to a query is returned to the User. This type of differential privacy is adopted when the Data generators trusts the data curator completely and leaves it to the curator the amount of noise to be added to the results. This type of privacy results is more accurate as it involves lesser noise.

.. figure:: https://user-images.githubusercontent.com/19529592/91381550-4ec2d400-e845-11ea-8f63-b7a3adb3fde8.png
    :alt: global
    :align: center
    :figclass: align-center

    Image Credits: Google Images

Formal Definition Of Differential Privacy
=========================================

In the book, “`The Algorithmic Foundations of Differential Privacy <https://www.cis.upenn.edu/~aaroth/Papers/privacybook.pdf>`_” by Cynthia Dwork and Aaron Roth. Differential Privacy is formally defined as:
.. glossary::
*A randomized algorithm M with domain N |X| is (ε, δ)-differentially private if for all S ⊆ Range(M) and for all x, y ∈ N |X| such that ∥x − y∥1 ≤ 1:*

 *Pr[M(x) ∈ S] ≤ exp(ε) Pr[M(y) ∈ S] + δ*

The Epsilon *(ε)* and *Delta(δ)* parameters measure the threshold for leakage.

* The Epsilon defines how different the actual actual data is from the queried data. If *ε=0*, exp(*ε*)=1 which means both the data are equal.

* The Delta is the probability that an information will accidentally be leaked as compared to the value of Epsilon. If  *δ=0*, that means no data is being leaked.

This when both Epsilon and Delta is 0, it is called Perfect-Privacy. The values are set in such a way so that the privacy is maintained. This set of values is known as Privacy-Budget.

Differential - Privacy In Real World
====================================

Differential Privacy ensures privacy of all sorts of data which can be used by anyone to draw insights which can help them run their business. In the present world, Differentially Private Data Analysis is widely used and these are implemented by using various libraries.

`PyDP <https://github.com/OpenMined/PyDP>`_ by OpenMined is a Python Wrapper for Differential Privacy which allows all sorts of users to use Differential Privacy in their Projects. Apart from this there are various other real-world cases of Differential Privacy from Medical Imaging to Geolocation search. These have been covered in this `blogpost <https://blog.openmined.org/use-cases-of-differential-privacy>`_  by OpenMined.

SOME OTHER LIBRARIES FOR DP

* `OpenDp  <https://github.com/opendifferentialprivacy>`_ by Harvard University and Microsoft
* `Diffprivlib <https://github.com/IBM/differential-privacy-library>`_  by IBM
* Google’s Differential Privacy `Library <https://github.com/IBM/differential-privacy-library>`_ .

DIFFERENTIAL PRIVACY IN USE

Top tech companies are using “Differential Privacy” in their day to day business for the privacy of data. Some of the use cases are here as follows:

* Uber

Uber, a popular ride-sharing company uses Differential Privacy in its practices. The company uses a method of Differential Privacy called “`elastic sensitivity <https://github.com/uber-archive/sql-differential-privacy>`_”, developed in the University of California at Berkeley. It uses mathematics to set limits on the number of statistical queries  the staff can conduct on traffic patterns and driver’s revenue. This method also ensures addition of noise in case the potential of a privacy breach is more severe.


* Apple

Apple also makes use of differential privacy to analyse user behaviour and improve user experience. Accessing private data such as browsing history, apps that we browse, words that we type etc can compromise user privacy. But these data are extremely useful when it comes to improving user experience. Apple makes use of “`Local Differential Privacy <https://machinelearning.apple.com/research/learning-with-privacy-at-scale>`_” algorithms which ensures that the raw data is randomized before sending it to the servers. This approach is implemented at scale across on millions of users and by harnessing this data various business decisions are taken.


* Google

Google also uses this novel approach to keep user data private to themselves and perform data analysis with that data to drive some of their core products. One such product is the Gboard (Google Keyboard), where it uses private data of the user to generate word suggestions. The method used is “Federated Learning” which decreases the reliance on the cloud and puts a strong focus on a user’s privacy. Rather than sending encrypted data to the servers, it downloads the current model on device and improves it by learning from the data on device. The updated model with the changes is sent to the cloud using encrypted communication. This is done at scale across all users and the updates from each user is immediately averaged with other updates to improve the shared model. In the year 2019, `Google open sourced the Differential Privacy  library <https://developers.googleblog.com/2019/09/enabling-developers-and-organizations.html>`_
for others to use.

Differential Privacy is playing an important role in building Privacy-protected Machine Learning solutions. PyDP is an effort to democratize this field. To know more about Differential Privacy and PyDP head over to our amazing blog series at `OpenMined Blog <https://blog.openmined.org>`_.




Further Reading
===============

* `Secure and Private AI Course on Udacity by Andrew Trask <https://www.udacity.com/course/secure-and-private-ai--ud185>`_

* `“The Algorithmic Foundations of Differential Privacy” by Cynthia Dwork and Aaron Roth <https://www.cis.upenn.edu/~aaroth/Papers/privacybook.pdf>`_

* `OpenMined Blogs on Differential Privacy <https://blog.openmined.org/tag/differential-privacy>`_
