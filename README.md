# Exercise-and-Analysis-to-Detecting-DGA

This repo was created with a mixture of information obtained from many different sources. I created this project for my 'text mining' class at school. It is purely educational.

# About

When users connect to a site that is thought to be legit, they enter the requested information on this site without realizing that the site is a fake site, and the attacker now has this user's private information. This type sites are created by some techniques such as ‘dga’ and are hidden by some methods. DGA, in short, are algorithmically generated domain names. Although the difference in the URL address is remarkable, for an inexperienced user on the subject, such pages are a good trap.

DGA fields have the following characteristics:

 - They have long and meaningless names

 - They are usually encoded or encrypted using the same cryptographic algorithms that both the malware client and the C&C server share, making them difficult to decode/decipher.

 - Thousands of DGA domains are created every day, but only a few are active or solvable, and this is known only to the malware client and C&C server.

 - Even when active, they have a short lifespan (usually only a few days), which makes them difficult to blacklist.

 - There are points where it is used instead of the DNS Tunneling tactic.

There are many studies in the literature on detecting Phishing Attacks [1]. The methods used by the studies developed for this purpose are different. In the literature, Natural Language Processing Based [2], Image Processing Based [3, 4], Machine Learning Based [4, 5], Rule Based [6], Whitelist – Blacklist Based [7].

 ![image](https://user-images.githubusercontent.com/36304333/192251118-4a978924-d51f-49aa-8791-0a04355aa193.png)

In this study, the term ‘Free URL’ is used to refer to the Subdomain Name and Path sections, which are domains that the attacker has full control over and can manipulate in order to mislead users.
An attacker can purchase any Domain Name that is not currently in use and use it for attack purposes. This part of the URL can only be set once. By making any changes in the Free URL field, the attacker can generate an unlimited number of URLs that he can use in phishing attacks.

# Datasets and Methods

There are technical details in the Jupyter Notebook, I have briefly summarized it here.

Two classes of information are needed to detect phishing attacks; 1) Legit URL, 2) Malicious URL.

The malicious URLs analyzed in this study were obtained from PhishTank [8], Zeus Botnet and Opendns phishing datasets. Alexa Dataset was used to obtain legal URLs.

You can see another domains datas in /data file.

Each element in the URL may contain some segregation marks within itself. For example, a distinction is made by using the “-” sign in the Domain Name in the URL ‘abc-company.com’. Similarly, it can be used with characters such as “ =, ?, & ” in the Path field. Before starting the URL preprocessing, words separated by any separating character for each URL are obtained and added to the word list to be analyzed. For this step used ‘tldextract’ tool from github [9].

The system was classified using the "length" and "entropy" values. The 'sklearn' python library was used for this step. Initially, the 'cross-validation score' was measured. Then, some classifier methods were tried and accuracy values were calculated.

After the analysis, new methods were sought to increase the accuracy rate. N-gram method is applied using both domains and dictionary dataset. Dictionary dataset taken from github [10].

Also, i tried 'markov chain' method. You can see details in /markov. 

# Conclusion 

The results show that the Random Forest Classifier has the most accuracy in both cases. AdaBoost Classifier values was decrease after n-gram modules. It’s weird but the cause was not investigated.

Some datasets are made by mathematical algorithms, and it's bad for testing. Domains which generated this way are same length and very different n-gram scores from legit domains.

Some domains are too long and have make sense words like ‘bipolardisorderdepressionanxiety’. For this type domains, we can separate word by word and analyze.

Consequently, the results can be further increased by adding new parameters to the algorithm. Such as ‘parsed word count’, ‘keyword similar’, ‘domain name similar’. Error analysis was not performed in this study. More efficient results can be obtained by performing error analysis. Long words was not parsed, again more efficient results can be obtained by doing this process.



# References

https://github.com/SuperCowPowers/data_hacking/tree/master/dga_detection

[1]	Garera, S., Provos, N., Chew, M., & Rubin, A. D. (2007,November). A framework for detection and measurement ofphishing attacks. In Proceedings of the 2007 ACM workshop onRecurring malcode (pp. 1-8). ACM. 

[2]	A. Stone, “Natural-language processing for intrusion detection,”Com- puter, vol. 40, no. 12, pp. 103 –105, dec. 2007.

[3]	A. Y. Fu, L. Wenyin, and X. Deng, “Detecting phishing webpages with visual similarity assessment based on earth mover’sdistance (emd),” IEEE Trans. Dependable Secur. Comput., vol.3, no. 4, pp. 301–311, Oct. 2006

[4]	F. Toolan and J. Carthy, “Phishing detection using classifierensembles,” in eCrime Researchers Summit, 2009. eCRIME’09., 20 2009-oct. 21 2009, pp. 1 –9.

[5]	S. Abu-Nimeh, D. Nappa, X. Wang, and S. Nair, “A comparisonof machine learning techniques for phishing detection,” inProceedings of the anti-phishing working groups 2nd annualeCrime researchers summit, ser. eCrime ’07. New York, NY,USA: ACM, 2007, pp. 60– 69. 

[6]	D. L. Cook, V. K. Gurbani, and M. Daniluk, “Phishwish: Astateless phishing filter using minimal rules,” in FinancialCryptography and Data Security, G. Tsudik, Ed. Berlin,Heidelberg: Springer-Verlag, 2008, pp. 182–186.

[7]	Y. Cao, W. Han, and Y. Le, “Anti-phishing based on automatedindividual white-list,” in DIM ’08: Proceedings of the 4th ACMworkshop on Digital identity management. New York, NY,USA: ACM, 2008, pp. 51–60.

[8]	https://www.phishtank.com/developer_info.php 

[9]	https://github.com/john-kurkowski/tldextract.git 

[10]	https://github.com/dwyl/english-words/blob/master/words.txt 
