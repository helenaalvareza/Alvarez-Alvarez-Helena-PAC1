se_object #per veure un summary de les dades

table(colData(se_object)$Class) #per identificar quantes mostres hi ha de cada classe

#Per determinar els valors perduts per mostra i matabòlit
missing_data <- colMeans(is.na(assay(se_object)))
barplot(missing_data, main = "Percentatge de valors perduts per mostra")
mean_missing_data <- mean(missing_data)
mean_missing_data
missing_data_1 <- rowMeans(is.na(assay(se_object)))
barplot(missing_data_1, main = "Percentatge de valors perduts per matabòlit")


#Per fer la PCA primer corretgim el objecte translocant perque hi hagi el 
#mateix número de files en la matriu i dataset. Addicionalment els valors que 
#son nuls esl posem com la mitja de cada metabòlit perque no donin biaix i 
#fem la PCA
corrected_data <- t(assay(se_object))
sum(is.na(corrected_data))
corrected_data[is.na(corrected_data)] <- apply(corrected_data, 2, mean, na.rm = TRUE)
corrected_data <- imputePCA(corrected_data, ncp = 2)
pca_result <- prcomp(corrected_data, scale = TRUE)
fviz_pca_ind(pca_result, label = "none", habillage = colData(se_object)$Class)