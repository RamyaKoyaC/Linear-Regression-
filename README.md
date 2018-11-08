# Linear-Regression-
Implementing a linear regression on WW-2 Temperature data 

```r
temperature <- read.csv("/storage/scratch2/rk0349/Summary of Weather.csv") # Loading data 
temperature<-temperature[1:500,] # Selecting only 500 rows of the data
fit <- lm(temperature$MeanTemp ~ temperature$MinTemp) # Fiting a linear model 
print(fit) # Printing the linear model equation 
summary(fit) # This includes the mse 
predictions <- predict(fit,temperature) # trying to predict with the fitted values 
head(predictions)
mse <- mean((temperature$MeanTemp - predictions)^2) # Finding the mean square error 
print(mse)
plot(temperature$MeanTemp, temperature$MinTemp) #PLotting x and y 
plot(predictions, temperature$MeanTemp)

set.seed(100)  # setting seed to reproduce results of random sampling
trainingRowIndex <- sample(1:nrow(temperature), 0.6*nrow(temperature))  # row indices for training data
trainingData <- temperature[trainingRowIndex, ]# model training data
trainingData
testData  <- temperature[-trainingRowIndex, ] #test data
testData
lmMod <- lm(temperature$MeanTemp ~ temperature$MinTemp, data=trainingData)  # build the model
print(lmMod)

tempPred <- predict(lmMod, testData) 
head(testData)
summary(lmMod)
head(tempPred)
AIC (lmMod)
plot(temperature$MinTemp,temperature$MeanxTemp, main="Rate of Change of Temperature ")
