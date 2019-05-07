#real label
real_label = []
count = -1
i = 0

a=len(Y_test)*6
for nb in range(a):
  if count == 5 :
    count = 0
    i += 1
  else:
    count += 1
  #print('count:',count)
  #print('i:',i)
  if (Y_test[i][count] == 1) : real_label.append(count)
    

#print('Prediction:',pred_label)
print('Y_test:',real_label)



#predicted label with specific threshold
pred_prob = model.predict(X_test)

result_2=[0]*len(Y_test)
i=0
j=0
while i < 6:
  print("图",i,':')
  while j<len(Y_test):
    result_2[j]=pred_prob[j][i]
    j+=1
  j=0
  i+=1
  print(result_2)

threshold=[0]*21
threshold[0]=0
i=1
while i<21:
  threshold[i]=threshold[i-1]+0.05
  i+=1
print(threshold)

#print('Prediction:',pred_prob)


#predicted label by default shreshold
pred_label = np.argmax(pred_prob, axis=1)
print(pred_label)


#9
#calculate TPR and FPR
'''TP=[[0]*21]*6
TN=[[0]*21]*6
FP=[[0]*21]*6
FN=[[0]*21]*6'''

TP=0
TN=0
FP=0
FN=0
X=[[0]*21]*6
Y=[[0]*21]*6

i=0
j=0
for th in range(len(threshold)):
  #print('threshold=',th*0.05)
  while i < 6:
    #print("图",i,':')
    while j<len(Y_test):
      if result_2[j]>=threshold[th] and real_label[j]==i:
        TP+=1
      elif result_2[j]<threshold[th] and real_label[j]!=i:
        TN+=1
      elif result_2[j]>=threshold[th] and real_label[j]!=i:
        FP+=1
      elif result_2[j]<threshold[th] and real_label[j]==i:
        FN+=1
      j+=1
      
      if (TN+FP)!=0:
        FPR=float(FP)/(TN+FP)
      else:
        FPR=-1
      if (TP+FN)!=0:
        TPR=float(TP)/(TP+FN)
      else:
        TPR=-1     
    #print('FP=',FP,'TN=',TN,'TP=',TP,'FN=',FN,'FPR=',FPR,'TPR=',TPR)
    #print('fpr',FPR)
    X[i][th]=FPR
    #print('x',X[i][th])
    Y[i][th]=TPR
    TP=0
    TN=0
    FP=0
    FN=0
    j=0
    i+=1
  i=0
  #print(" ")
  
print('X=',X)
print('Y=',Y)


#draw ROC curve
#import matplotlib.pyplot as plt
#import numpy as np

for class_nb in range(nb_classes):
  print('class_nb:',class_nb)
  x=X[class_nb]
  y=Y[class_nb]
  plt.xlabel("False Positive Rate")
  plt.ylabel("True Positive Rate")
  plt.plot(x,y)
  plt.show()
