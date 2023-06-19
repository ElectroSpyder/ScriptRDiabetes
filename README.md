# ScriptRDiabetes
Scripts que se ejecutan sobre software R usando un set de datos de diabetes
library(mongolite)

connection_string = 'mongodb+"aqui va la url de mongodb"/CancerDB'

Coleccion = mongo(collection="DiabetesCollection", db="DiabetesDB", url=connection_string)

Coleccion$count()

Datos.Diabetes = Coleccion$find()

Datos.Diabetes$Diabetes =ifelse(test = Datos.Diabetes$Outcome = 1, yes = "Si", no = "No")
Datos.Diabetes$Diabetes = as.factor(Datos.Diabetes$Diabetes)
Datos.Diabetes$Outcome = NULL
set.seed(123)
indice.Train = sample(1:nrow(Datos.Diabetes), nrow(Datos.Diabetes)/2, replace = FALSE)
Dato.Train = Datos.Diabetes[indice.Train,]
Dato.Prueba= Datos.Diabetes[-indice.Train,]
Dato.Clasificacion = tree(formula = Diabetes~., data = Dato.Train)

summary(Dato.Clasificacion)
head(Dato.Train, 3)
head(Dato.Prueba, 3)

par(mar = c(1,1,1,1))
plot(x = Dato.Clasificacion, type = "proportional")
text(x = Dato.Clasificacion, splits = TRUE, pretty = 0, cex = 0.7, col = "firebrick")
Dato.Predicciones = predict(Dato.Clasificacion, newdata = Dato.Prueba, type="class")
table(Dato.Predicciones,Dato.Prueba$Diabetes)
summary(Dato.Predicciones)
nrow(Dato.Predicciones)
nrow(Dato.Prueba)

table(Dato.Clasificacion,Dato.Train$Diabetes, type="class")
