# african_genetic

This is a r-script for analysing the Tishkoff 2009 dataset. I'm trying to compute some kind of genetic diversity
and see how that correlates with Murdoch dataset variables (cousin marriage for example). 

if (!require(psych)) {install.packages("psych"); require(bda)} 
if (!require(ggplot2)) {install.packages("ggplot2"); require(ggplot2)} 
if (!require(ggfortify)) {install.packages("ggfortify"); require(ggfortify)} 

raw_data<-read.csv("~/science/Genotyping data used for The Genetic Structure and History .csv")

name_list<-raw_data[,3]

#subset the data to match EA
keep_list<-c("Sandawe","Iraqw","Turu","Mbugwe","Rangi","Maasai (Tanzania)",
             "Pare","Bakola","Bedzan","Ngumba","Kanuri","Giziga",
             "Baggara","Kotoko","Bamoun","Banen","Bafia","Batanga",
             "Podokwo","Hazara","Sindhi","Pathan","Burusho","Mbuti",
             "Druze","Cambodian","Japanese","Russian","Mandenka",
             "Yoruba","Yakut","Pima","Miao","Daur","Hezhen","Xibo",
             "Tu","Basque","Adygei","Igbo","Igala","Gwari","Dinka",
             "Datoga","Sukuma","Gogo","Fiome/Gorowa","Fang","Mabea",
             "South Tikar","North Tikar","Ntumu","Massa","Ashanti",
             "Brong","Maasai Mumonyot","Maasai Il'gwesi","Samburu",
             "Samba'a","Dorobo","Yoruba (CEPH)","Burji","Luo","Kikuyu",
             "Okiek","Nandi","Turkana","Konso","Laka","Kanembou",
             "Mbum","Gbaya","Fulani Mbororo","Kongo","Baluba","Dioula",
             "Nuer","Nyimang","Sara (various)","Venda","Xhosa","Koma",
             "Beta Israel","Dogon","Temani","Bengali","Gujarat","Kashmiri",
             "Parsi","Punjabi","Tamil","Telugu")

for (i in keep_list){
  if (i %in% name_list == FALSE){
    print ("not matching")
    print (i)
  }
}# check to see if data entrance is correct

african_data<-raw_data[ which(raw_data$population.name %in% keep_list==TRUE),]



african.pca<-prcomp(african_data[,-c(1,2,3)],center=TRUE,scale.=TRUE) #standard pca function in r.
plot(african.pca, type = "l") # check variance explained. Not looking ideal, but we'll go with 2 pc solution since we want to visualize potential clustering patterns.

autoplot(african.pca, data = african_data,colour="population.name", cex=0.3)


#------------------------------------------------#

