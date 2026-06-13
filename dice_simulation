
import pandas as pd
import random
import time
import matplotlib.pyplot as plt

def main():
    rolls = input("Please enter the number of rolls. if i was you, i would've picked 1000000 or more : ")
    try:
        rolls = int(rolls)
    except ValueError:
        print("Please enter a valid integer for the number of rolls.")
        return main()
    
    if rolls > 0:
        start_time = time.time()

        # Create a DataFrame with the specified number of rows, each representing a set of three dice rolls using list comprehensions to generate random integers between 1 and 6 for each roll.
        df = pd.DataFrame({
            'number': range(1, rolls + 1),
            'first_roll': [random.randint(1, 6) for _ in range(1, rolls + 1)],
            'second_roll': [random.randint(1, 6) for _ in range(1, rolls + 1)],
            'third_roll': [random.randint(1, 6) for _ in range(1, rolls + 1)],
        }) 

        # Count the frequency of each possible combination (from 3 to 18) and sort the results by the sum value in ascending order.
        df['result'] = df['first_roll'] + df['second_roll'] + df['third_roll'] 
        stat = df['result'].value_counts().sort_index(ascending=True) 

        # Calculate the probabilities of each sum by dividing the frequency of each sum by the total number of rolls to get the relative frequencies.
        probabilities = pd.DataFrame({
            'probability': stat / stat.sum()
        })
        
        print(probabilities.merge(stat, on='result', left_index=True, right_index=True, how='left').sort_index(ascending=True))

        
        # The average
        average = df['result'].mean() 
        print(f"Average: {average:.2f}") 

        # The standard deviation
        std = df['result'].std() 
        print(f"Standard Deviation: {std:.2f}") 

        prob_within_one_std = (
            ((df['result'] >= average - std) &
            (df['result'] <= average + std))
        ).mean()
        print(f"Probability within one standard deviation: {prob_within_one_std * 100:.2f}%") 

        prob_within_two_std = (
            ((df['result'] >= average - 2 * std) &
            (df['result'] <= average + 2 * std))
        ).mean()
        print(f"Probability within two standard deviations: {prob_within_two_std * 100:.2f}%") 

        prob_within_three_std = (
            ((df['result'] >= average - 3 * std) &
            (df['result'] <= average + 3 * std))
        ).mean()
        print(f"Probability within three standard deviations: {prob_within_three_std * 100:.2f}%") 

        print(f"Total rolls: {len(df)}") 

        # histogram
        df['result'].hist(bins=range(2, 20), color='peachpuff', edgecolor='black', density=True , align='left', alpha=0.85)

        # Mean line
        plt.axvline(average, linestyle='--', linewidth= 1.5, color='royalblue', label=f'Mean = {average:.2f}')

        # ±1 std
        plt.axvline(average - std, linestyle=':', linewidth= 1.5, color='steelblue', label='±1std')
        plt.axvline(average + std, linestyle=':', linewidth= 1.5, color='steelblue')

        # ±2 std
        plt.axvline(average - 2 * std, linestyle='-.', linewidth= 1.5, color='lightsteelblue', label='±2std')
        plt.axvline(average + 2 * std, linestyle='-.', linewidth= 1.5, color='lightsteelblue')

        plt.xlabel('Dice Sum')
        plt.ylabel('Density')
        
        plt.style.use('dark_background')
        plt.xticks(range(3, 19))
        plt.legend()
        plt.title(f'Distribution of Three Dice Sums ({rolls:,} rolls)')
        plt.show()

        end_time = time.time()
        print(f"Execution time: {(end_time - start_time):.2f} seconds") # Print the total execution time of the code to evaluate its performance.
    
if __name__ == "__main__":    
    main()