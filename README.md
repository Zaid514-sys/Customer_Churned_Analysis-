    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt 
    %matplotlib inline 
    import seaborn as sns

    df = pd.read_csv(r"C:\Users\ALZAID SHAIKH\Downloads\Customer-Churn-analysis-main\Customer-Churn-analysis-main\Customer Churn.csv")
    df
    df.head()

    df.info()

    # Replace blank with 0 as tenure is 0 and no total charges are recorded
    
      df['TotalCharges'] = df['TotalCharges'].replace(" ","0")
      df['TotalCharges'] = df['TotalCharges'].astype("float")

      df.isnull().sum()

      df.describe()

    df["customerID"].duplicated().sum()

    # Here we have converted 0 and 1 values for senior_citizen to yes/No to make is easier to understand

    def conv(Value):
    if Value == 1:
        return "yes"
    else:
        return "No"
        
    df['SeniorCitizen'] = df['SeniorCitizen'].apply(conv)

    df.head(30)  

    ax = sns.countplot(x = 'Churn',data=df)
    plt.title('Customer churn')
    
    for p in ax.patches:
        ax.annotate(f'{p.get_height()}', (p.get_x() + p.get_width() / 2, p.get_height()), 
        ha='center', va='bottom', fontsize=12, color='black')

        ![image](https://github.com/user-attachments/assets/57ad972d-b97e-4edb-be8f-8d4a88e3d34f)


    gb = df.groupby("Churn").agg(Count =('Churn','count'))
    gb
    
    # Here we can see 73.5% customers are still with  services and 26.5 % customers have churn out 

    plt.figure(figsize=(5,5))
    gb = df.groupby("Churn").agg(Count=('Churn', 'count')).reset_index()
    plt.pie(gb['Count'], labels=gb['Churn'], autopct='%1.1f%%')
    plt.title('percentage for churned customers', fontsize = 20)
    plt.show

    ![image](https://github.com/user-attachments/assets/caef8040-7706-4a98-9159-8e573d7b6526)

    sns.countplot(df["gender"],data=df,hue="Churn")
    plt.title("Churn by gender")
    plt.show()
    ![image](https://github.com/user-attachments/assets/0e3c681c-10b3-4edb-a2a2-ec96104c065b)

    ax = sns.countplot(df["SeniorCitizen"],data=df)
    for p in ax.patches:
        ax.annotate(f'{p.get_height()}', (p.get_x() + p.get_width() / 2, p.get_height()), 
                    ha='center', va='bottom', fontsize=12, color='black')
    plt.title("Count of SeniorCitizen ")
    plt.show()

    ![image](https://github.com/user-attachments/assets/9aab26f5-dac0-4572-9541-f62835c7c982)

    sns.countplot(df["SeniorCitizen"],data=df,hue="Churn")
    plt.title("Churn by SeniorCitizen")
    plt.show()

    ![image](https://github.com/user-attachments/assets/20593db1-5155-483f-b5b4-db6dd0b3ed01)

    total_counts = df.groupby('SeniorCitizen')['Churn'].value_counts(normalize=True).unstack() * 100

    # Plot
    fig, ax = plt.subplots(figsize=(4, 4))  # Adjust figsize for better visualization
    
    # Plot the bars
    total_counts.plot(kind='bar', stacked=True, ax=ax, color=['#1f77b4', '#ff7f0e'])  # Customize colors if desired
    
    # Add percentage labels on the bars
    for p in ax.patches:
        width, height = p.get_width(), p.get_height()
        x, y = p.get_xy()
        ax.text(x + width / 2, y + height / 2, f'{height:.1f}%', ha='center', va='center')
    
    plt.title('Churn by Senior Citizen (Stacked Bar Chart)')
    plt.xlabel('SeniorCitizen')
    plt.ylabel('Percentage (%)')
    plt.xticks(rotation=0)
    plt.legend(title='Churn', bbox_to_anchor = (0.9,0.9))  # Customize legend location
    
    plt.show()

    ![image](https://github.com/user-attachments/assets/488747ad-72ed-4fcf-ae89-6441ec29e713)

    # Compargtive  a greater percentage of the people in senior citizen have churned 

    counts, bins = np.histogram(df["tenure"], bins=50)
    # Plot with plt.bar for better separation
    plt.bar(bins[:-1], counts, width=np.diff(bins), edgecolor="black", align="edge")

    ![image](https://github.com/user-attachments/assets/83214f06-37fc-48ae-a072-241a1d2d25a6)








    
      
      
