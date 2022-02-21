# stat_hw

import statistics
from scipy.stats import norm, expon
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

#1
    theta = np.random.uniform(0,1)
    
    for n in [20,50,100,500]:
        s = 0
        mad1 = 0
        mad2 = 0
        for i in range(100):
            uni_data = np.random.uniform(0,theta,size=n)
            t1 = (n+1)/n*np.max(uni_data)
            t2 = 2*statistics.mean(uni_data)
            ad1 = np.abs(t1 - theta)
            ad2 = np.abs(t2 - theta)
            if ad2 < ad1:
                s+=1
            mad1 += ad1/n
            mad2 += ad2/n
        print(s,'сколько раз вторая оценка была ближе', mad1, 'mad1', mad2, 'mad2')
    
<img width="756" alt="Снимок экрана 2022-02-21 в 10 09 12" src="https://user-images.githubusercontent.com/60537367/154905770-74d0d78e-245d-4197-9755-e57224abfe13.png">

#2

    for n in [20,50,100,500]:
        numb = []
        for i in range(1000):
            uni_data = np.random.uniform(0, theta, size=n)
            t2 = 2 * statistics.mean(uni_data)
            numb.append(n**0.5*(t2 - theta))
        f = sns.histplot(numb, stat='density')
        x0, x1 = f.get_xlim()
        x_pdf = np.linspace(x0, x1)
        y_pdf = norm.pdf(x_pdf, scale=np.std(uni_data)**0.5)
        f.plot(x_pdf, y_pdf, 'r')
        fig = f.get_figure()
        fig.savefig('hist_t2'+str(n))
        plt.close()
        
![hist_t220](https://user-images.githubusercontent.com/60537367/154909542-68e01d38-09c8-4030-b8b9-ea256bac6adc.png)

![hist_t250](https://user-images.githubusercontent.com/60537367/154909552-e4c5ee78-0c70-4a8f-a122-2b0033f0e336.png)

![hist_t2100](https://user-images.githubusercontent.com/60537367/154909558-048593af-0772-46ad-8455-de7fcf28e67e.png)

![hist_t2500](https://user-images.githubusercontent.com/60537367/154909563-7c066a11-5f5d-4d11-9571-50aeefd72c37.png)


#3

    for n in [20,50,100,500]:
        numb = []
        for i in range(1000):
            uni_data = np.random.uniform(0, theta, size=n)
            t1 = (n+1)/n*np.max(uni_data)
            numb.append(n**0.5*(t1 - theta))
        f = sns.histplot(numb, stat='density')
        x0, x1 = f.get_xlim()
        x_pdf = np.linspace(x0, x1)
        y_pdf = norm.pdf(x_pdf, scale=np.std(uni_data)**0.5)
        f.plot(x_pdf, y_pdf, 'r')
        f.figure.savefig('hist_t1' + str(n))
        plt.close()
        
![hist_t120](https://user-images.githubusercontent.com/60537367/154909442-2bc6b235-4a70-4989-ae1a-5325a7d37a32.png)

![hist_t150](https://user-images.githubusercontent.com/60537367/154909456-a54b11ba-6a42-48ac-a8fa-2947551adb18.png)

![hist_t1100](https://user-images.githubusercontent.com/60537367/154909470-b032a92b-0677-4513-b1e0-cb5d4aac48b2.png)

![hist_t1500](https://user-images.githubusercontent.com/60537367/154909478-a87ab680-84c9-4e5a-bc5b-5e417c1b919d.png)


#4

for n in [20,50,100,500]:
    numb = []
    for i in range(1000):
        uni_data = np.random.uniform(0, theta, size=n)
        t1 = np.max(uni_data)
        numb.append(n*(t1 - theta))
    f = sns.histplot(numb, stat='density')
    x0, x1 = f.get_xlim()
    x_pdf = np.linspace(x0, x1)
    y_pdf = expon.pdf(x_pdf)
    f.plot(x_pdf, y_pdf)
    fig = f.get_figure()
    fig.savefig('hist_max' + str(n))
    plt.close()
