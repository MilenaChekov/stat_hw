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
    nor = []
    for i in range(1000):
        uni_data = np.random.uniform(0, theta, size=n)
        t2 = 2 * statistics.mean(uni_data)
        numb.append(n**0.5*(t2 - theta))
        nor.append(n**0.5*(t2 - theta)/np.std(uni_data)**0.5)
    f = sns.histplot(numb, stat='density')
    x0, x1 = f.get_xlim()
    x_pdf = np.linspace(x0, x1)
    y_pdf = norm.pdf(x_pdf, scale=np.std(uni_data)**0.5)
    f.plot(x_pdf, y_pdf, 'r')
    sns.kdeplot(nor)
    fig = f.get_figure()
    fig.savefig('hist_t2'+str(n))
    plt.close()
    
    ![hist_t220](https://user-images.githubusercontent.com/60537367/154905826-f51cb7b9-f2cb-42b0-ace9-40c274eac072.png)

![hist_t250](https://user-images.githubusercontent.com/60537367/154905837-d78cd4bb-e5bf-4830-aab1-c12ba0a586e7.png)

![hist_t2100](https://user-images.githubusercontent.com/60537367/154905858-5cea5212-5875-4a6d-a6a7-0825e7e57277.png)

![hist_t2500](https://user-images.githubusercontent.com/60537367/154905867-bad5c2fc-02c1-4ec8-968e-219ec6b8edcd.png)

#3

for n in [20,50,100,500]:
    numb = []
    nor = []
    for i in range(1000):
        uni_data = np.random.uniform(0, theta, size=n)
        t1 = (n+1)/n*np.max(uni_data)
        numb.append(n**0.5*(t1 - theta))
        nor.append(n**0.5*(t1 - theta)/np.std(uni_data)**0.5)
    f = sns.histplot(numb, stat='density')
    x0, x1 = f.get_xlim()
    x_pdf = np.linspace(x0, x1)
    y_pdf = norm.pdf(x_pdf, scale=np.std(uni_data)**0.5)
    f.plot(x_pdf, y_pdf, 'r')
    sns.kdeplot(nor)
    f.figure.savefig('hist_t1' + str(n))
    plt.close()
    
    ![hist_t120](https://user-images.githubusercontent.com/60537367/154905942-bd086881-89d5-42ed-9384-c70a6126d9b6.png)

![hist_t150](https://user-images.githubusercontent.com/60537367/154905955-bbd9a59d-0fab-40b5-b90a-ee92b9b34880.png)

![hist_t1100](https://user-images.githubusercontent.com/60537367/154905970-59b29dc9-4af4-4be3-a831-5d883f3724e7.png)

![hist_t1500](https://user-images.githubusercontent.com/60537367/154905976-731c6142-9b78-4ed4-8c1e-bedcda1a2c6b.png)

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
