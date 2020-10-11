# R_jot

#install.packages("leaflet") 
#install.packages("maptools") 
#install.packages("rgdal") 
#system("conda install -c conda-forge r-rgdal")
#install.packages("XML")
#install.packages("RCurl")
#install.packages("rlist")

library(leaflet) 
library(sp) 
library(raster) 
library(maptools)
library(rgdal)
#library(rvest)
library(readxl)
library(XML)
library(RCurl)
library(rlist)

html_fname = "/home/ec2-user/SageMaker/jot_SGM/Onion_Nashik_2015_2020_Oct10.html"
tables = readHTMLTable(html_fname)
tables <- list.clean(tables, fun = is.null, recursive = FALSE)
n.rows <- unlist(lapply(tables, function(t) dim(t)[1]))
jot = (tables$cphBody_GridPriceData)
                        
#Read plot 
#getwd()
IND_adm1_fname = "/home/ec2-user/SageMaker/jot_SGM/India_gadm/gadm36_IND_1.shp"
IND_adm2_fname = "/home/ec2-user/SageMaker/jot_SGM/India_gadm/gadm36_IND_2.shp"
#ogrInfo(IND_adm2_fname)
#ogrListLayers(IND_adm2_fname)
IND_adm1_sp <- rgdal::readOGR(dsn=IND_adm1_fname, verbose = F)
IND_adm2_sp <- rgdal::readOGR(dsn=IND_adm2_fname, verbose = F)
plot(IND_adm2_sp)
plot(IND_adm1_sp, add = T, border = 'red')
