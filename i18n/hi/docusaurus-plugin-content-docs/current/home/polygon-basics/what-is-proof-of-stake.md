---
id: what-is-proof-of-stake
title: भागीदारी का सबूत क्या है?
description: वैलिडेटरों पर निर्भर एक सहमति अल्गोरिथम.
keywords:
  - docs
  - matic
  - polygon
  - stake
  - delegate
  - validate
  - pos
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# स्टेक का सबूत (PoS) {#proof-of-stake-pos}

भागीदारी का सबूत (पॉस) सार्वजनिक ब्लॉकचेन के लिए सहमति अल्गोरिथम की एक श्रेणी है जो नेटवर्क में एक वैलिडेटर के आर्थिक [स्टेक](/docs/maintain/glossary#staking) पर निर्भर करता है.

कार्य के सबूत (PoW) आधारित सार्वजनिक सार्वजनिक ब्लॉकचेन में, अल्गोरिथम उन प्रतिभागियों को रिवॉर्ड प्रदान करता है जो ट्रांज़ैक्शन को वैलिडेट करने और नए ब्लॉक बनाने के लिए क्रिप्टोग्राफ़िक पहेलियों को हल करते हैं. PoW ब्लॉकचेन उदाहरण: Bitcoin, पहले Ethereum.

पॉस आधारित सार्वजनिक ब्लॉकचेन में, वैलिडेटरों का एक समूह बारी-बारी से प्रस्ताव करता है और अगले ब्लॉक पर मतदान करता है. हर वैलिडेटर के वोट का महत्त्व उनके डिपाज़िट — [स्टेक](/docs/maintain/glossary#staking) पर निर्भर करता है. पॉस (PoS) के महत्वपूर्ण लाभों में सुरक्षा, केंद्रीकरण का कम जोखिम और ऊर्जा दक्षता शामिल हैं. पॉस ब्लॉकचेन के उदाहरण: एथ2, पॉलीगॉन.

सामान्य तौर पर, एक पॉस अल्गोरिथम इस प्रकार दिखता है. ब्लॉकचेन वैलिडेटरों के एक समूह की निगरानी करता है, और जो कोई भी ब्लॉकचैन की आधार क्रिप्टोकरेंसी (एथेरेयम के मामले में, एथेर) रखता है, एक विशेष प्रकार की ट्रांज़ैक्शन को भेजकर एक वैलिडेटर बन सकता है जो अपने एथेर को डिपाज़िट में लॉक कर देता है. नए ब्लॉक बनाने और सहमत होने की प्रक्रिया फिर एक आम सहमति अल्गोरिथम के माध्यम से की जाती है जिसमें सभी मौजूदा वैलिडेटर भाग ले सकते हैं.

सहमति अल्गोरिथम कई प्रकार के होते हैं, और सहमति अल्गोरिथम में भाग लेने वाले वैलिडेटरों को रिवॉर्ड प्रदान करने के कई तरीके हैं, इसलिए भागीदारी के सबूत कई "प्रकार" हैं. अल्गोरिथम के दृष्टिकोण से, दो प्रमुख प्रकार हैं: चेन-आधारित पॉस और [BFT](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance)स्टाइल पॉस.

**चेन आधारित भागीदारी के सबूत** में, अल्गोरिथम छद्म-यादृच्छिक रूप से हर समय स्लॉट के दौरान एक वैलिडेटर चुनता है (उदाहरण के लिए 10 सेकंड की हर अवधि एक समय स्लॉट हो सकती है), और उस वैलिडेटर को सिंगल ब्लॉक बनाने का ज़्यादाार प्रदान करता है, और इस ब्लॉक को किसी पिछले ब्लॉक को इंगित करना चाहिए (आमतौर पर पिछली सबसे लंबी चेन के अंत में मौजूद ब्लॉक को), और इसलिए समय के साथ ज़्यादाांश ब्लॉक एक निरंतर बढ़ती चेन में परिवर्तित हो जाते हैं.

**BFT स्टाइल भागीदारी के सबूत** में, वैलिडेटरों को **बेतरतीब ढंग से** ब्लॉक्स का *प्रस्ताव करने* का अधिकार दिया जाता है, लेकिन सहमति *व्यक्त करते हुए कि कौन सा ब्लॉक प्रामाणिक है*, ऐसा एक मल्टी-राउंड प्रक्रिया के माध्यम से किया जाता है, जहां हर वैलिडेटर हर राउंड के दौरान कुछ विशिष्ट ब्लॉक के लिए "वोट" भेजता है, और प्रक्रिया के अंत में सभी (ईमानदार और ऑनलाइन) वैलिडेटर स्थायी रूप से इस बात पर सहमत होते हैं कि निर्धारित ब्लॉक चेन का हिस्सा है या नहीं. नोट करें कि ब्लॉक अभी भी *एक साथ चेन में जुड़े* हो सकते हैं; मुख्य अंतर यह है कि एक ब्लॉक पर सहमति एक ब्लॉक के भीतर आ सकती है, और यह इसके बाद की चेन की लंबाई या साइज़ पर निर्भर नहीं करती है.

ज़्यादा जानकारी के लिए, [https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ) का उल्लेख करें.

यह भी देखें:

* [डेलीगेटर](/docs/maintain/glossary#delegator)
* [वैलिडेटर](/docs/maintain/glossary#validator)