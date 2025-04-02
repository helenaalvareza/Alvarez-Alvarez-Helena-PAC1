#Separem les dades de la base de dades en dos objectes,un amb la informació de 
#les mostres i l'altre amb la informació dels metabòlits
data_path <- "GastricCancer_NMR.xlsx"
data_df <- read_excel(data_path, sheet = "Data")
peak_df <- read_excel(data_path, sheet = "Peak")

#per prepara les dades per SummarizedExperimment, primer fem una matriu amb 
#les columnes metabòliques
metabolite_data <- as.matrix(data_df[, 5:ncol(data_df)])  
rownames(metabolite_data) <- data_df$SampleID 
metabolite_data <- t(metabolite_data)  #trasposem la matriu perque hi hagi el mateix número de files

#Després creem un dataframe amb la informació sobre les mostres
sample_info <- data_df[, 1:4]  
rownames(sample_info) <- data_df$SampleID
sample_info <- as.data.frame(sample_info)  
rownames(sample_info) <- sample_info$SampleID  

#I un altre DataFrame amb la informació dels metabolits
feature_info <- data.frame(peak_df[, c("Name", "Label")])  
rownames(feature_info) <- peak_df$Name

#Cree, l'objecte SummarizedExperiment assignant a cada element una matriu o dataset
se_object <- SummarizedExperiment(
  assays = list(counts = metabolite_data),
  colData = sample_info,
  rowData = feature_info
)

#guardem l'objecte en format .rda
save(se_object, file = "SummarizedExperiment_GastricCancer.Rda")
