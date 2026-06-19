# Upload file in Colab
from google.colab import files
uploaded = files.upload()

# Read Dataset
df = pd.read_csv("student_info.csv")

# ==========================
# BASIC DATA EXPLORATION
# ==========================

print("DATASET SHAPE")
print(df.shape)

print("\nCOLUMN NAMES")
print(df.columns)

print("\nFIRST 5 RECORDS")
print(df.head())

print("\nDATASET INFORMATION")
df.info()

print("\nMISSING VALUES")
print(df.isnull().sum())

print("\nSTATISTICAL SUMMARY")
print(df.describe())

# ==========================
# SCORE ANALYSIS
# ==========================

print("\nAVERAGE SCORES")

print("Math Score :", df['math_score'].mean())
print("Reading Score :", df['reading_score'].mean())
print("Writing Score :", df['writing_score'].mean())

# ==========================
# RESULT ANALYSIS
# ==========================

print("\nPASS / FAIL COUNT")

print(df['final_result'].value_counts())

# ==========================
# GENDER WISE ANALYSIS
# ==========================

gender_scores = df.groupby('gender')[
    ['math_score','reading_score','writing_score']
].mean()

print("\nGENDER WISE AVERAGE SCORES")
print(gender_scores)

# ==========================
# ATTENDANCE ANALYSIS
# ==========================

attendance_result = df.groupby(
    'final_result'
)['attendance_rate'].mean()

print("\nAVERAGE ATTENDANCE BY RESULT")
print(attendance_result)

# ==========================
# TOP 10 MATH STUDENTS
# ==========================

top_math = df[
    ['student_id','name','math_score']
].sort_values(
    by='math_score',
    ascending=False
).head(10)

print("\nTOP 10 STUDENTS IN MATH")
print(top_math)

# ==========================
# VISUALIZATION 1
# PASS VS FAIL
# ==========================

plt.figure(figsize=(6,4))

df['final_result'].value_counts().plot(
    kind='bar'
)

plt.title("Pass vs Fail")
plt.xlabel("Result")
plt.ylabel("Count")

plt.show()

# ==========================
# VISUALIZATION 2
# AVERAGE SCORES
# ==========================

avg_scores = [
    df['math_score'].mean(),
    df['reading_score'].mean(),
    df['writing_score'].mean()
]

plt.figure(figsize=(6,4))

plt.bar(
    ['Math','Reading','Writing'],
    avg_scores
)

plt.title("Average Scores")
plt.ylabel("Average Marks")

plt.show()

# ==========================
# VISUALIZATION 3
# ATTENDANCE DISTRIBUTION
# ==========================

plt.figure(figsize=(6,4))

plt.hist(
    df['attendance_rate'],
    bins=10
)

plt.title("Attendance Distribution")
plt.xlabel("Attendance Rate")
plt.ylabel("Frequency")

plt.show()

# ==========================
# VISUALIZATION 4
# GENDER WISE SCORES
# ==========================

gender_scores.plot(
    kind='bar',
    figsize=(8,5)
)

plt.title("Gender Wise Average Scores")
plt.ylabel("Average Marks")

plt.show()

# ==========================
# CORRELATION MATRIX
# ==========================

print("\nCORRELATION MATRIX")

print(
    df[
        [
            'math_score',
            'reading_score',
            'writing_score',
            'attendance_rate',
            'study_hours'
        ]
    ].corr()
)
