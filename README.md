Sample-Stata
============

clear 
set more off
cd "I:\group\TCORS-P50\Data\GYTS\Data"

log using "I:\group\TCORS-P50\Data\GYTS\Logs\get_rawdata1", replace

***********************
*** raw EIU price data:
***********************
/*
use data/initial\EIU\EIUprices, replace
collapse (mean) price* marlboro*, by(country)
gen city = "natl"
append using data/initial\EIU\EIUprices
drop if city == ""
replace country = "china" if country == "China PR"
replace country = "czechrepublic" if country == "Czech Rep"
replace country = "cotedivoire" if country == "Ivory Coast"
replace country = "southkorea" if country == "Korea Rep"
replace country = "philippines" if country == "Philipines"
replace country = "russianfederation" if country == "Russia"
replace country = "republicofsrpska" if country == "Serbia"
replace country = subinstr(country," ","",.)
replace country = lower(country)
replace city = subinstr(city," ","",.)
replace city = lower(city)
reshape long price marlboro, i(country city) j(year)
drop if price == .
rename city eiucity
sort country eiucity year
tempfile prices
save `prices', replace
*/
***********************
*** raw GYTS data:
***********************

#delimit;
global AFR "benin_atlantquelittoral
benin_borgoualibori
botswana
burkinafaso_bobodioulasso
burkinafaso_ouagadougou
burundi
cameroon_centraldistrict
cameroon_outsideyaounde
cameroon_yaounde
capeverde
cenafricanrep_bangui
comoros
congo
cotedivoire
cotedivoire_abidjan
cotedivoire_villesud
demrepcongo_kinshasa
equatorialguinea
eritrea
ethiopia_addisababa
gambia_banjul
ghana
guinea
guineabissau_bissau
kenya
lesotho
liberia_monrovia
madagascar
malawi
malawi_blantyre
malawi_lilongwe
mali
mali_bamako
mauritania
mauritius
mauritius_rodrigues
mozambique_maputocity
namibia
niger
nigeria_abuja
nigeria_crossriverstate
rwanda
saotomeandprincipe
senegal
seychelles
sierraleone_westernarea
southafrica
swaziland
tanzania_arusha
tanzania_daressalaam
tanzania_kilimanjaro
togo
uganda
uganda_arua
uganda_kampala
uganda_mpigi
zambia
zambia_chongweandluangwa
zambia_kafue
zambia_lusaka
zimbabwe_harare
zimbabwe_mandb
zimbabwe_manicaland
algeria_constantine
algeria_oran
algeria_setif";

global EM "egypt
gazastrip
gazastrip_unrwa
iran
iraq_baghdad
iraq_kurdistan
jordan
jordan_unrwa
kuwait
lebanon
lebanon_unrwa
libya
morocco
oman
pakistan
pakistan_karachi
pakistan_kasur
pakistan_peshawar
pakistan_quetta
qatar
saudiarabia
saudiarabia_riyadh
somalia_somaliland
sudan
syria
syria_unrwa
tunisia
unitedarabemirates
westbank
westbank_unrwa
yemen
afghanistan_kabul
bahrain
djibouti";

global EU "azerbaijan
belarus
bosniaherzegovina
bosniaherzegovina_fed
bosniaherzegovina_srpska
bulgaria
croatia
cyprus
czechrepublic
estonia
georgia
greece
hungary
italy
kazakhstan
kosovo
kyrgyzstan
latvia
lithuania
macedonia
moldova
montenegro
poland
poland_rural
poland_urban
romania
russianfederation
russianfederation_moscow
russianfederation_sarov
sanmarino
serbia
slovakia
slovenia
tajikistan
turkey
ukraine
ukraine_kiev
uzbekistan_tashkent
albania
armenia";

global ROTA "argentina_capitalfederal
argentina_capitalfederal
bahamas
barbados
belize
bolivia_cochabamba
bolivia_lapaz
bolivia_santacruz
brazil_alagoas
brazil_aracaju
brazil_belem
brazil_boavista
brazil_cataguases
brazil_curitiba
brazil_espiritosanvit
brazil_florianopolis
brazil_fortaleza
brazil_goiania
brazil_joaopessoa
brazil_macapa
brazil_matogrossodosul
brazil_natal
brazil_palmas
brazil_palmitos
brazil_paraiba
brazil_riodejaneiro
brazil_riograndedonorte
brazil_riograndedosul
brazil_salvador
brazil_saoluis
brazil_tocantins
chile_concepcion
chile_coquimbo
chile_santiago
chile_valparaiso
colombia_bogota
costarica
cuba
cuba_havana
dominica
dominicanrepublic
ecuador_guayaquil
ecuador_quito
ecuador_zamora
elsalvador
grenada
guatemala
guatemala_chimaltenango
guatemala_guatemalacity
guyana
haiti_portauprince
honduras
honduras_sanpedro
honduras_tegucigalpa
jamaica
mexico
mexico_chetumal
mexico_chilpancingo
mexico_ciudadjuarez
mexico_cuernavaca
mexico_culiacan
mexico_durango
mexico_guadalajara
mexico_hermosillo
mexico_juarez
mexico_leon
mexico_merida
mexico_mexicocity
mexico_monterrey
mexico_nuevolaredo
mexico_oaxaca
mexico_puebla
mexico_tapachula
mexico_tepic
mexico_tijuana
mexico_toluca
mexico_veracruz
mexico_zacatecas
montserrat_
nicaragua
nicaragua_bluefields
nicaragua_puertocabezas
nicaragua_centro
nicaragua_centromanagua
nicaragua_pacifico
panama
paraguay
paraguay_altoparana
paraguay_amambay
paraguay_asuncion
paraguay_central
peru
peru_huancayo
peru_icacity
peru_lima
peru_tarapoto
peru_trujillo
saintkittsandnevis
saintlucia
saintvincent
suriname
trinidadandtobago
uruguay
uruguay_colonia
uruguay_maldonado
uruguay_montevideo
uruguay_rivera
venezuela
venezuela_barinas
venezuela_cojedes
venezuela_lara
venezuela_monagas
venezuela_nuevaesparta
venezuela_tachira
venezuela_yaracuy
venezuela_zulia
virginislands_british
antiguaandbarbuda
argentina
argentina_buenosaires";

global SEA "bhutan
bhutan
easttimor_
india
india_ahmedabad
india_andrapradesh
india_arunachalpradesh
india_assam
india_bihar
india_chandigarh
india_delhi
india_goa
india_gujarat
india_gujaratwithamedabad
india_haryana
india_himichalpradesh
india_jammuandkashmir
india_karnaraka
india_kerala
india_madhyapradesh
india_maharashtra
india_manipur
india_meghalaya
india_mizoram
india_nagaland
india_orissa
india_punjab
india_rajasthan
india_sikkim
india_tamilnadu
india_tripura
india_uttarpradesh
india_uttranchal
india_westbengal
indonesia
indonesia_bekasi
indonesia
indonesia_medan
indonesia_surakarta
maldives
maldives_urban
myanmar
nepal
nepal_biratnagar
srilanka
thailand
bangladesh
bangladesh_dhaka
bhutan";

global WP "china_shanghai
china_tianjin
china_zhuhai
cookislands
fiji
guam
hongkong
kiribati
laos
laos_luangprabang
laos_luangprabangprovince
laos_savannakhet
laos_vientianecapital
laos_vientianeprovince
macau
malaysia
marshallislands
micronesia
mongolia
newcaledonia
newzealand
niue
papuanewguinea
philippines
samoa
singapore
solomonislands
southkorea
tonga
tuvalu
vanuatu
vietnam
vietnam_denang
vietnam_haiphong
vietnam_hanoi
vietnam_hochiminh
vietnam_tuenguang
cambodia
china_chongqing
china_macau
china_puyang
china_shandong";
#delimit cr

foreach r in AFR EM EU ROTA SEA WP {
	foreach i in ${`r'} {
		forvalues j = 1999/2011 {
			cap clear
			cap use "I:\group\TCORS-P50\Data\GYTS\Data/`r'/`i'_`j'"
			cap renvars _all, lower
			
			/*cap confirm var cr11, exact
			if !_rc {
			}
			else {
			cap save "I:\group\TCORS-P50\Data\GYTS\Data\diffvar/`r'/`i'_`j'", replace
			}
			*/
			
			cap gen year = "`j'"
			cap destring year, replace
			cap gen loc = "`i'"
			cap split loc, parse(_)
			cap rename loc1 country
			cap rename loc2 city
			cap drop loc
			cap gen city = "natl"
			gen region = "`r'"
						
			*** define TRY ***
			
			cap gen try_v1 = . /*cigs*/
			cap replace try_v1 = cr1
			*AFR*
			cap replace try_v1 = zbr4  if country == "zimbabwe" & year == 2008
			*EM*
			cap replace try_v1 = tnr1  if country == "tunisia" & year == 2001
			*EU*
			cap replace try_v1 = bgr1  if country == "blugaria" & year == 2002
			cap replace try_v1 = lvr1  if country == "latvia" & year == 2002
			*SEA*
			cap replace try_v1 = npr1  if country == "nepal"
			cap gen try_v2 = . /*tobacco*/
			*EM*
			cap replace try_v2 = aer12 if country == "unitedarabemirates" & year == 2002
			cap replace try_v2 = inr1  if country == "india"
			*SEA*
			cap replace try_v2 = inr1  if country == "bangladesh" & year == 2004
			cap replace try_v2 = inr1  if country == "india" & year < 2006
			cap replace try_v2 = mmr1  if country == "myanmar" & year == 2001
			cap replace try_v2 = mmr1  if country == "myanmar" & year == 2004
			cap replace try_v2 = npr1  if country == "nepal" & year == 2001
			cap replace try_v2 = .     if country == "nepal" & year == 2003
			cap replace try_v2 = npr1  if country == "nepal" & year == 2004
			cap gen try_v3 = . /*hseyleik*/
			*SEA*
			cap replace try_v3 = mmr1  if country == "myanmar" & year == 2004
			
			*** define TRYOLD ***

			cap gen tryold_v1 = . /*smoking*/
			cap replace tryold_v1 = cr2
			
			*AFR*
			cap replace tryold_v1 = cir2  if country == "cotedivoire" & year == 2003
			cap replace tryold_v1 = etr2  if country == "ethiopia" & city == "addisababa"
			cap replace tryold_v1 = lsr2  if country == "lesotho" & year == 2008
			cap replace tryold_v1 = ngr2  if country == "nigeria" & city == "crossriverstate"
			cap replace tryold_v1 = scr2  if country == "seychelles" & year == 2007
			cap replace tryold_v1 = zar6  if country == "southafrica" & year > 1999
			*EM*
			cap replace tryold_v1 = pbr3  if country == "gazastrip" & year == 2000
			cap replace tryold_v1 = pkr3  if country == "pakistan" & year == 2008
			cap replace tryold_v1 = sor3  if country == "somalia" & year == 2004
			cap replace tryold_v1 = tnr3  if country == "tunisia" & year == 2001
			cap replace tryold_v1 = pbr3  if country == "westbank" & year == 2000
			*EU*
			cap replace tryold_v1 = cyr8  if country == "cyprus" & year == 2005
			cap replace tryold_v1 = hur2  if country == "hungary" & year == 2008
			*ROTA*
			cap replace tryold_v1 = cor3  if country == "colombia" & year == 2001
			cap replace tryold_v1 = xrr6  if country == "costarica" & year == 2002
			cap replace tryold_v1 = dmr2  if country == "dominica" & year == 2000
			cap replace tryold_v1 = par2  if country == "panama" & year == 2002
			cap replace tryold_v1 = mxr2  if country == "mexico" & year > 2000
			*SEA*
			cap replace tryold_v1 = idr2  if country == "indonesia" & year == 2004
			cap replace tryold_v1 = inr2  if country == "india" & city == "natl"
			*WP*
			cap replace tryold_v1 = .     if country == "newzealand" & year == 2010			
			cap gen tryold_v2 = . /*tobacco*/
			*SEA*
			cap replace tryold_v2 = inr2  if country == "bangladesh" & year == 2004
			cap replace tryold_v2 = ind2  if country == "indonesia" & year == 2004
			cap replace tryold_v2 = mmr1  if country == "myanmar" & year == 2001
			cap replace tryold_v2 = npr2  if country == "nepal" & & year < 2007
			cap replace tryold_v2 = inr2  if country == "india" & city != "natl"
			cap gen tryold_v3 = . /*snuff*/
			*SEA*
			cap replace tryold_v3 = inr19 if country == "india" & city == "natl"
			cap gen tryold_v4 = . /*hseyleik*/
			*SEA*
			cap replace tryold_v4 = mmr1  if country == "myanmar" & year == 2004

			*** define SMOKEDAYS ***

			cap gen smokedays_v1 = . /*cigs*/
			cap replace smokedays_v1 = cr3
			*AFR*
			cap replace smokedays_v1 = snr3  if country == "senegal" & year == 2002
			cap replace smokedays_v1 = zbr7  if country == "zimbabwe" & year == 2008
			*EM*
			cap replace smokedays_v1 = kwr3  if country == "kuwait" & year == 2009
			cap replace smokedays_v1 = lbr3  if country == "lebanon" & year == 2005
			cap replace smokedays_v1 = sdr6  if country == "sudan" & year == 2005
			cap replace smokedays_v1 = tnr3  if country == "tunisia" & year == 2001
			*EU*
			cap replace smokedays_v1 = lvr6  if country == "latvia" & year == 2002
			*SEA*
			cap replace smokedays_v1 = inr6  if country == "india" & city != "natl"
			cap replace smokedays_v1 = mmr4  if country == "myanmar" & year == 2001
			*WP*
			cap replace smokedays_v1 = khr3  if country == "cambodia" & year == 2003
			cap replace smokedays_v1 = .     if country == "newzealand" & year == 2010
			cap gen smokedays_v2 = . /*tobacco*/
			*SEA*
			cap replace smokedays_v2 = inr6  if country == "bangladesh" & year == 2004
			cap replace smokedays_v2 = inr6  if country == "india" & city != "natl"
			cap replace smokedays_v2 = mmr4  if country == "myanmar" & year == 2001
			cap replace smokedays_v2 = npr5  if country == "nepal" & year < 2007
			cap gen smokedays_v3 = . /*snuff or chewing tobacco*/
			*SEA*
			cap replace smokedays_v3 = inr7  if country == "bangladesh" & year == 2004
			cap replace smokedays_v3 = inr7  if country == "india" & city != "natl"
			cap replace smokedays_v3 = inr20 if country == "india" & city == "natl"
			cap replace smokedays_v3 = npr6  if country == "nepal" & year < 2007
			cap gen smokedays_v4 = . /*bidis or hseyleik*/
			*SEA*
			cap replace smokedays_v4 = inr13 if country == "india" & city == "natl"
			cap replace smokedays_v4 = mmr3  if country == "myanmar" & year == 2004
			
			*** define CIGPERDAY ***

			cap gen cigperday_v1 = ./*cigs*/
			cap replace cigperday_v1 = cr4
			*AFR*
			cap replace cigperday_v1 = cmr4  if country == "cameroon" & year == 2008
			cap replace cigperday_v1 = cvr4  if country == "capeverde" & year == 2007
			cap replace cigperday_v1 = snr4  if country == "senegal" & year == 2002
			cap replace cigperday_v1 = tzr4  if country == "tanzania" & year == 2008
			cap replace cigperday_v1 = zbr8  if country == "zimbabwe" & year == 2008
			*EM*
			cap replace cigperday_v1 = lbr4  if country == "lebanon" & year == 2005
			cap replace cigperday_v1 = lbr4  if country == "lebanon" & year == 2011
			*EU*
			cap replace cigperday_v1 = cyr10 if country == "cyprus"
			cap replace cigperday_v1 = lvr7  if country == "latvia" & year == 2002
			cap replace cigperday_v1 = uar5  if country == "ukraine" & city == "kiev"
			*ROTA*
			cap replace cigperday_v1 = brr4  if country == "brazil"
			cap replace cigperday_v1 = clr4  if country == "chile" & year > 2000
			*SEA*
			cap replace cigperday_v1 = idr4  if country == "indonesia" & city == "bekasi"
			cap replace cigperday_v1 = idr4  if country == "indonesia" & city == "medan"
			cap replace cigperday_v1 = lkr7  if country == "srilanka" & year == 1999
			cap replace cigperday_v1 = lkr7  if country == "srilanka" & year == 2003
			*WP*
			cap replace cigperday_v1 = cnr4  if country == "china" & city == "macau"
			cap replace cigperday_v1 = lar4  if country == "laos" & year == 2007
			cap replace cigperday_v1 = ncr4  if country == "newcaledonia"
			cap replace cigperday_v1 = phr4  if country == "philippines" & year == 2007
			cap replace cigperday_v1 = phr4  if country == "philippines" & year == 2011
			cap gen cigperday_v2 = ./*bidis*/
			*SEA*
			cap replace cigperday_v2 = inr9  if country == "bangladesh" & year == 2004
			cap replace cigperday_v1 = mmr5  if country == "myanmar" & year == 2004 /*hseyleik included with bidis here*/
			cap replace cigperday_v2 = inr9  if country == "india" & city != "natl"
			cap replace cigperday_v2 = inr14 if country == "india" & city == "natl"
			cap replace cigperday_v2 = npr8  if country == "nepal"

			*** define POCKET ***
	
			cap gen pocketid = .
			*AFR*
			cap replace pocketid = dzr9  if country == "algeria"
			cap replace pocketid = bjr9  if country == "benin"
			cap replace pocketid = bwr15 if country == "botswana" & year == 2001
			cap replace pocketid = bfr9  if country == "burkinafaso" & year < 2009
			cap replace pocketid = bir9  if country == "burundi"
			cap replace pocketid = cvr16 if country == "capeverde"
			cap replace pocketid = kmr9  if country == "comoros"
			cap replace pocketid = cgr9  if country == "congo" & year == 2006
			cap replace pocketid = cir9  if country == "cotedivoire" & year == 2003
			cap replace pocketid = err9  if country == "eritrea" & year == 2006
			cap replace pocketid = etr9  if country == "ethiopia"
			cap replace pocketid = ghr9  if country == "ghana" & year < 2009
			cap replace pocketid = ker10 if country == "kenya" & year == 2001
			cap replace pocketid = ker9  if country == "kenya" & year == 2007
			cap replace pocketid = lsr9  if country == "lesotho" & year == 2002
			cap replace pocketid = mwr9  if country == "malawi" & year == 2000
			cap replace pocketid = mwr11 if country == "malawi" & year == 2005
			cap replace pocketid = cr9   if country == "mali" & year == 2001
			cap replace pocketid = mlr9  if country == "mali" & year == 2008
			cap replace pocketid = mrr9  if country == "mauritania"
			cap replace pocketid = mur21 if country == "mauritius" & year == 2003
			cap replace pocketid = mzr9  if country == "mozambique"
			cap replace pocketid = nar9  if country == "namibia" & year == 2004
			cap replace pocketid = ner17 if country == "niger"
			cap replace pocketid = ngr9  if country == "nigeria" & year == 2004
			cap replace pocketid = snr9  if country == "senegal"
			cap replace pocketid = scr10 if country == "seychelles"
			cap replace pocketid = zar14 if country == "southafrica" & year == 2002
			cap replace pocketid = zar14 if country == "southafrica" & year == 2011
			cap replace pocketid = szr9  if country == "swaziland" & year < 2009
			cap replace pocketid = tzr9  if country == "tanzania" & year == 2003
			cap replace pocketid = tgr9  if country == "togo" & year == 2002
			cap replace pocketid = ugr9  if country == "uganda" & year == 2002
			cap replace pocketid = zmr9  if country == "zambia" & year == 2002
			cap replace pocketid = zbr9  if country == "zimbabwe" & year == 2003
			*EM*
			cap replace pocketid = afr9  if country == "afghanistan"
			cap replace pocketid = djr9  if country == "djibouti" & year == 2003
			cap replace pocketid = egr9  if country == "egypt" & year == 2005
			cap replace pocketid = pbr9  if country == "gazastrip" & year == 2005
			cap replace pocketid = irr9  if country == "iran" & year == 2003
			cap replace pocketid = irq9  if country == "iraq" & year == 2006
			cap replace pocketid = jor9  if country == "jordan" & year == 2003
			cap replace pocketid = jor9  if country == "jordan" & year == 2007
			cap replace pocketid = kwr9  if country == "kuwait" & year == 2005
			cap replace pocketid = lbr10 if country == "lebanon" & year == 2001
			cap replace pocketid = lbr9  if country == "lebanon" & year == 2005
			cap replace pocketid = lbr9  if country == "lebanon" & year == 2011
			cap replace pocketid = lyr9  if country == "libya" & year < 2010
			cap replace pocketid = mar8  if country == "morocco" & year < 2010
			cap replace pocketid = omr9  if country == "oman" & year == 2003
			cap replace pocketid = pkr9  if country == "pakistan" & year < 2008
			cap replace pocketid = qar9  if country == "qatar" & year == 2004
			cap replace pocketid = sar9  if country == "saudiarabia" & year < 2010
			cap replace pocketid = sor9  if country == "somalia" & year == 2004
			cap replace pocketid = cr9   if country == "somalia" & year == 2007
			cap replace pocketid = sdr10 if country == "sudan" & year == 2001
			cap replace pocketid = sdr15 if country == "sudan" & year == 2005
			cap replace pocketid = syr9  if country == "syria" & year == 2002
			cap replace pocketid = tnr9  if country == "tunisia" & year == 2001
			cap replace pocketid = aer9  if country == "unitedarabemirates" & year == 2005
			cap replace pocketid = pbr9  if country == "westbank" & year == 2005
			cap replace pocketid = yer9  if country == "yemen" & year == 2003
			*EU*
			cap replace pocketid = brg9  if country == "bulgaria" & year == 2002
			cap replace pocketid = cr17  if country == "croatia" & year == 2003
			cap replace pocketid = czr10 if country == "czechrepublic" & year < 2010
			cap replace pocketid = grr16 if country == "greece"
			cap replace pocketid = hur15 if country == "hungary" & year == 2003
			cap replace pocketid = lvr13 if country == "latvia" & year == 2002
			cap replace pocketid = ltr9  if country == "lithuania"
			cap replace pocketid = plr11 if country == "poland" & year == 1999
			cap replace pocketid = plr21 if country == "poland" & year == 2003
			cap replace pocketid = ror16 if country == "romania" & year == 2004
			cap replace pocketid = rur10 if country == "russianfederation" & year == 2002
			cap replace pocketid = rur16 if country == "russianfederation" & year == 2004
			cap replace pocketid = trr16 if country == "turkey"
			cap replace pocketid = cr17  if country == "ukraine" & year < 2011
			*ROTA*
			cap replace pocketid = agr11 if country == "antiguaandbarbuda" & year < 2009
			cap replace pocketid = arr9  if country == "argentina" & year == 2000
			cap replace pocketid = bsr9  if country == "bahamas" & year == 2000
			cap replace pocketid = cr9   if country == "bahamas" & year == 2004
			cap replace pocketid = bbr9  if country == "bardabos" & year == 2002
			cap replace pocketid = bzr9  if country == "belize" & year == 2002
			cap replace pocketid = bor9  if country == "bolivia"
			cap replace pocketid = brr16 if country == "brazil" & year >= 2005
			cap replace pocketid = brr14 if country == "brazil" & year < 2005
			cap replace pocketid = clr9  if country == "chile" & year < 2008
			cap replace pocketid = cor10 if country == "colombia"
			cap replace pocketid = cur9  if country == "cuba"
			cap replace pocketid = dmr9  if country == "dominica" & year < 2009
			cap replace pocketid = dor9  if country == "dominicanrepublic"
			cap replace pocketid = ecr9  if country == "equador"
			cap replace pocketid = cr9   if country == "elsalvador" & year == 2003
			cap replace pocketid = gdr12 if country == "grenada" & year == 2000
			cap replace pocketid = gdr9  if country == "grenada" & year == 2004
			cap replace pocketid = gtr14 if country == "guatemala" & year == 2002
			cap replace pocketid = gyr11 if country == "guyana" & year < 2010
			cap replace pocketid = htr9  if country == "haiti"
			cap replace pocketid = hnr12 if country == "honduras"
			cap replace pocketid = jmr9  if country == "jamaica" & year < 2010
			cap replace pocketid = mxr9  if country == "mexico" & year < 2011
			cap replace pocketid = mxr13 if country == "mexico" & city == "monterrey" & year == 2000
			cap replace pocketid = msr9  if country == "montserrat"
			cap replace pocketid = nir9  if country == "nicaragua"
			cap replace pocketid = par9  if country == "panama" & year == 2002
			cap replace pocketid = pyr10 if country == "paraguay" & year == 2003
			cap replace pocketid = per9  if country == "peru" & year < 2007
			cap replace pocketid = knr9  if country == "saintkittsandnevis" & year == 2002
			cap replace pocketid = lcr12 if country == "saintlucia" & year == 2000
			cap replace pocketid = lcr9  if country == "saintlucia" & year == 2007
			cap replace pocketid = vcr9  if country == "saintvincent" & year < 2011
			cap replace pocketid = srr9  if country == "suriname" & year < 2009
			cap replace pocketid = ttr10 if country == "trinidadandtobago" & year < 2011
			cap replace pocketid = uyr10 if country == "uruguay"
			cap replace pocketid = ver9  if country == "venezuela" & year == 2001
			cap replace pocketid = ver9  if country == "venezuela" & year == 2003
			cap replace pocketid = vgr9  if country == "virginislands"
			*SEA*
			cap replace pocketid = bdr16 if country == "bangladesh" & year == 2004
			cap replace pocketid = bdr9  if country == "bangladesh" & year == 2007
			cap replace pocketid = btr9  if country == "bhutan" & year < 2009
			cap replace pocketid = btr10 if country == "bhutan" & year == 2009
			cap replace pocketid = tpr10 if country == "easttimor" & year == 2006
			cap replace pocketid = inr20 if country == "india" & city != "natl"
			cap replace pocketid = idr9  if country == "indonesia" < 2009
			cap replace pocketid = mvr9  if country == "maldives" & year < 2011
			cap replace pocketid = mmr15 if country == "myanmar" & year == 2001
			cap replace pocketid = mmr16 if country == "myanmar" & year == 2004
			cap replace pocketid = npr20 if country == "nepal" & year < 2007
			cap replace pocketid = thr9  if country == "thailand" & year == 2005
			cap replace pocketid = thr55 if country == "thailand" & year == 2009
			*WP*
			cap replace pocketid = khr9  if country == "cambodia" & year == 2003
			cap replace pocketid = cr9   if country == "cambodia" & year == 2010
			cap replace pocketid = cnr9  if country == "china" & year == 2005
			cap replace pocketid = cnr10 if country == "china" & city == "macau" & year == 2005
			cap replace pocketid = mor8  if country == "china" & city == "macau" & year == 2001
			cap replace pocketid = ckr10 if country == "cookislands" & year == 2003
			cap replace pocketid = hkr13 if country == "hongkong" & year == 2009
			cap replace pocketid = lar9  if country == "laos" & year == 2003
			cap replace pocketid = lar9  if country == "laos" & year == 2011
			cap replace pocketid = mor8  if country == "macau" & year == 2001
			cap replace pocketid = cnr10 if country == "macau" & year == 2005
			cap replace pocketid = myr14 if country == "malaysia" & year == 2003
			cap replace pocketid = mhr9  if country == "marshallislands" & year == 2009
			cap replace pocketid = fmr9  if country == "micronesia" & year == 2007
			cap replace pocketid = mnr9  if country == "mongolia" & year == 2003
			cap replace pocketid = nzr7  if country == "newzealand" & year == 2007
			cap replace pocketid = pgr9  if country == "papuanewguinea" & year == 2007
			cap replace pocketid = phr9  if country == "philippines" & year < 2007
			cap replace pocketid = wsr9  if country == "samoa" & year == 2007
			cap replace pocketid = sgr10 if country == "singapore" & year == 2000
			cap replace pocketid = krr9  if country == "southkorea" & year == 2005
			cap replace pocketid = tvr9  if country == "tuvalu" & year == 2006
			cap replace pocketid = vur9  if country == "vanuatu" & year == 2007
			cap replace pocketid = vnr11 if country == "vietnam" & year == 2003
			
			*** define NOBUY ***

			cap gen nobuy_v1 = . /*cigs*/
			cap replace nobuy_v1 = cr10
			cap replace nobuy_v1 = cr7   if year    >= 2008 | year == 1999
			*AFR*
			cap replace nobuy_v1 = mwr7  if country == "malawi" & year == 2009
			cap replace nobuy_v1 = ner12 if country == "niger"
			cap replace nobuy_v1 = scr11 if country == "seychelles" & year == 2002
			cap replace nobuy_v1 = cr7   if country == "seychelles" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "uganda" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "zambia" & year == 2007
			*EM*
			cap replace nobuy_v1 = lbr10 if country == "lebanon" & year == 2005
			cap replace nobuy_v1 = cr7   if country == "iran" & year == 2007
			cap replace nobuy_v1 = omr10 if country == "oman" & year == 2003
			cap replace nobuy_v1 = cr7   if country == "qatar" & year == 2007
			cap replace nobuy_v1 = sdr12 if country == "sudan" & year == 2001
			cap replace nobuy_v1 = cr7   if country == "syria" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "tunisia" & year == 2007
			*EU*
			cap replace nobuy_v1 = .     if region  == "EU"
			cap replace nobuy_v1 = cr10  if country == "bulgaria" & year == 2002
			cap replace nobuy_v1 = cr14  if country == "bulgaria" & year == 2008
			cap replace nobuy_v1 = cr10  if country == "czechrepublic" & year <= 2010
			cap replace nobuy_v1 = eer18 if country == "estonia" & year == 2003
			cap replace nobuy_v1 = cr18  if country == "kyrgyzstan" & year == 2004
			cap replace nobuy_v1 = cr10  if country == "latvia" & year == 2002
			cap replace nobuy_v1 = cr10  if country == "lithuania" & year <= 2008
			cap replace nobuy_v1 = cr14  if country == "lithuania" & year == 2008
			cap replace nobuy_v1 = cr7   if country == "poland" & year == 1999
			cap replace nobuy_v1 = cr7   if country == "russianfederation" & year == 1999
			cap replace nobuy_v1 = cr10  if country == "russianfederation" & year == 2002
			cap replace nobuy_v1 = cr18  if country == "turkey" & year == 2003
			cap replace nobuy_v1 = cr7   if country == "ukraine" & year == 1999
			cap replace nobuy_v1 = cr18  if country == "ukraine" & year == 2005
			*ROTA*
			cap replace nobuy_v1 = cr7   if country == "argentina" & year == 2007
			cap replace nobuy_v1 = bsr10 if country == "bahamas" & year == 2000
			cap replace nobuy_v1 = cr7   if country == "barbados" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "colombia" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "ecuador" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "peru" & year == 2007
			cap replace nobuy_v1 = vcr10 if country == "saintvincent" & year == 2000
			cap replace nobuy_v1 = ver32 if country == "venezuela" year == 2010
			*SEA*
			cap replace nobuy_v1 = cr7   if region  == "SEA" & year >= 2007
			cap replace nobuy_v1 = cr10  if region  == "SEA" & year == 2011
			cap replace nobuy_v1 = idr7  if country == "indonesia" & year == 2009
			cap replace nobuy_v1 = cr7   if country == "laos" & year == 2007
			cap replace nobuy_v1 = cr7   if country == "mongolia" & year == 2007
			cap replace nobuy_v1 = mmr16 if country == "myanmar" & year == 2001
			cap replace nobuy_v1 = cr10  if country == "srilanka" & year == 1999
			cap replace nobuy_v1 = cr7   if country == "vietnam" & year == 2007
			*WP*
			cap replace nobuy_v1 = cr10  if country == "cambodia" & year == 2010
			cap replace nobuy_v1 = cnr11 if country == "china" & city == "macau" & year == 2005
			cap replace nobuy_v1 = cr10  if country == "guam" year == 2011
			cap replace nobuy_v1 = cr7   if country == "laos" year == 2007
			cap replace nobuy_v1 = cr7   if country == "mongolia" year == 2007
			cap replace nobuy_v1 = cr10  if country == "newzealand" year == 2008
			cap replace nobuy_v1 = cr10  if country == "philippines" year == 2011
			cap replace nobuy_v1 = cr7   if country == "vietnam" year == 2007
			cap gen nobuy_v2 = . /*tobacco*/
			*EU*
			cap replace nobuy_v2 = cr18  if region  == "EU" & year >= 2000
			cap replace nobuy_v2 = cr10  if region  == "EU" & year == 2002
			cap replace nobuy_v2 = cr14  if region  == "EU" & year >= 2008
			cap replace nobuy_v2 = .     if nobuy_v2 != .
			cap replace nobuy_v2 = cr18  if country == "hungary" & year == 2008
			*SEA*
			cap replace nobuy_v2 = inr22 if country == "bangladesh" & year == 2004
			cap replace nobuy_v2 = npr21 if country == "nepal" & year == 2001
			cap replace nobuy_v2 = npr21 if country == "nepal" & year == 2004
			cap replace nobuy_v2 = inr22 if country == "india" & city != "natl"
			cap replace nobuy_v2 = inr16 if country == "india" & city == "natl"
			cap gen nobuy_v3 = . /*snuff*/
			*SEA*
			cap replace nobuy_v3 = inr23 if country == "india" & city == "natl"
			cap gen nobuy_v4 = . /*hseyleik*/
			*SEA*
			cap replace nobuy_v4 = mmr17 if country == "myanmar" & year == 2004

			*** define OTHER ***

			cap gen other_v1 = . /*tobacco other than cigarettes*/
			cap replace other_v1 = cr11
			cap replace other_v1 = cr8   if year    == 1999
			cap replace other_v1 = .     if year    >= 2008
			*AFR*
			cap replace other_v1 = bir11 if country == "burundi" & year == 2008
			cap replace other_v1 = gqr11 if country == "equatorialguinea" & year == 2008
			cap replace other_v1 = ghr11 if country == "ghana" & year == 2009
			cap replace other_v1 = mrr11 if country == "mauritania" & year == 2009
			cap replace other_v1 = mur11 if country == "mauritius" & year == 2003
			cap replace other_v1 = ner19 if country == "niger" & year == 2009
			cap replace other_v1 = .     if country == "seychelles" & year == 2007
			cap replace other_v1 = zar16 if country == "southafrica" & year >= 2008
			cap replace other_v1 = .     if country == "uganda" & year == 2007
			cap replace other_v1 = .     if country == "zambia" & year == 2007
			*EM*
			cap replace other_v1 = .     if country == "gazastrip" & year == 2000
			cap replace other_v1 = .     if country == "iran"
			cap replace other_v1 = iqr11 if country == "iraq" & year == 2006
			cap replace other_v1 = jor8  if country == "jordan" & year == 1999
			cap replace other_v1 = lbr18 if country == "lebanon" & year == 2001
			cap replace other_v1 = lbr17 if country == "lebanon" & year == 2005
			cap replace other_v1 = .     if country == "qatar" & year == 2007
			cap replace other_v1 = syr11 if country == "syria" & year == 2002
			cap replace other_v1 = syr62 if country == "syria" & year == 2007
			cap replace other_v1 = .     if country == "tunisia" & year == 2007
			cap replace other_v1 = aer17 if country == "unitedarabemirates" & year == 2002
			cap replace other_v1 = .     if country == "westbank" & year == 2000
			*EU*
			cap replace other_v1 = .     if region  == "EU" & year != 2002 & year != 1999
			cap replace other_v1 = c11   if country == "czechrepublic" & year == 2007
			cap replace other_v1 = czr7  if country == "czechrepublic" & year == 2011
			cap replace other_v1 = ltr11 if country == "lithuania" & year == 2009
			*ROTA*
			cap replace other_v1 = .     if region  == "ROTA" & year >= 2008
			cap replace other_v1 = cr9   if country == "argentina" & year == 2007
			cap replace other_v1 = cr9   if country == "barbados" & year == 2007
			cap replace other_v1 = cr11  if country == "brazil" & year == 2007
			cap replace other_v1 = clr15 if country == "chile" & year == 2008
			cap replace other_v1 = cor13 if country == "colombia" & year == 2007
			cap replace other_v1 = xrr14 if country == "costarica" & year == 2008
			cap replace other_v1 = dmr11 if country == "dominica" & year == 2000
			cap replace other_v1 = ecr11 if country == "ecuador" & year == 2007
			cap replace other_v1 = gtr11 if country == "guatemala" & year == 2008
			cap replace other_v1 = pyr12 if country == "paraguay" & year == 2008
			cap replace other_v1 = per11 if country == "peru" & year == 2007
			cap replace other_v1 = cr11  if country == "saintlucia" & year == 2007
			cap replace other_v1 = vcr11 if country == "saintvincent" & year == 2000
			cap replace other_v1 = cr11  if country == "saintvincent" & year == 2007
			cap replace other_v1 = ttr12 if country == "trinidadandtobago" & year == 2007
			cap replace other_v1 = ver11 if country == "venezuela" & year == 2008
			*SEA*
			cap replace other_v1 = .     if country == "bangladesh" & year == 2004
			cap replace other_v1 = .     if country == "bangladesh" & year == 2007
			cap replace other_v1 = btr18 if country == "bhutan" & year < 2009 & btr17 == 1
			cap replace other_v1 = .     if country == "india"
			cap replace other_v1 = idr8  if country == "indonesia" & year "2009"
			cap replace other_v1 = idr9  if country == "indonesia" & year "2009" & idr9 == 1
			cap replace other_v1 = mvr13 if country == "maldives" & year == 2007
			cap replace other_v1 = .     if country == "myanmar"
			cap replace other_v1 = npr17 if country == "nepal" & year == 2007
			cap replace other_v1 = cr11  if country == "srilanka" & year == 1999
			cap replace other_v1 = .     if country == "srilanka" & year == 2007			
			*WP*
			cap replace other_v1 = .     if country == "cookislands" & year == 2003
			cap replace other_v1 = cr8   if country == "cookislands" & year == 2008
			cap replace other_v1 = fjr17 if country == "fiji" & year >= 2005
			cap replace other_v1 = lar11 if country == "laos" & year >= 2007
			cap replace other_v1 = mhr11 if country == "marshallislands" & year == 2009
			cap replace other_v1 = .     if country == "mongolia" & year == 2007
			cap replace other_v1 = cr11  if country == "newzealand" & year == 2008
			cap replace other_v1 = nzr7  if country == "newzealand" & year == 2010
			cap replace other_v1 = cr8   if country == "niue" & year == 2010
			cap replace other_v1 = .     if country == "singapore" & year == 2000
			cap replace other_v1 = sbr17 if country == "solomonislands" & year == 2008
			cap replace other_v1 = vnr13 if country == "vietnam"			
			cap gen other_v2 = . /*smoked tobacco*/
			*AFR*
			cap replace other_v2 = cr8   if region  == "AFR" & year >= 2008
			cap replace other_v2 = .     if region  == "AFR" & year >= 2008 & other_v1 != .
			cap replace other_v2 = cgr8  if country == "congo" & year == 2009
			cap replace other_v2 = mwr9  if country == "malawi" & year == 2009
			cap replace other_v2 = .     if country == "mauritius" & year == 2008
			cap replace other_v2 = str8  if country == "saotomeandprincipe" & year == 2010
			cap replace other_v2 = cr8   if country == "seychelles" & year == 2007
			cap replace other_v2 = cr8   if country == "uganda" & year == 2007
			cap replace other_v2 = cr8   if country == "zambia" & year == 2007
			*EM*
			cap replace other_v2 = cr8   if region  == "EM" & year == 2008 & other_v1 != .
			cap replace other_v2 = djr8  if country == "djibouti" & year == 2009
			cap replace other_v2 = cr8   if country == "iran" & year == 2007
			cap replace other_v2 = cr8   if country == "qatar" & year == 2007
			cap replace other_v2 = cr8   if country == "tunisia" & year == 2007
			*ROTA*
			cap replace other_v2 = cr9   if region == "ROTA" & year >= 2009
			cap replace other_v2 = cr9   if country == "belize" & year == 2008
			cap replace other_v2 = cr8   if country == "elsalvador" & year == 2009
			cap replace other_v2 = gyr13 if country == "guyana" & year == 2010
			cap replace other_v2 = cr8   if country == "panama" & year == 2008
			cap replace other_v2 = ttr9  if country == "trinidadandtobago" & year == 2011
			*SEA*
			cap replace other_v2 = cr8   if country == "srilanka" & year == 2007
			cap replace other_v2 = thr8  if country == "thailand" & year == 2009
			cap replace other_v2 = btr18 if country == "bhutan" & year == 2009 & btr17 == 1
			cap replace other_v2 = cr8   if country == "easttimor" & year == 2009
			cap replace other_v2 = cr8   if country == "myanmar" & year == 2007
			cap replace other_v2 = mmr18 if country == "myanmar" & year == 2011
			cap replace other_v2 = npr3  if country == "nepal" & year < 2007
			cap replace other_v2 = npr17 if country == "nepal" & year == 2007
			cap replace other_v2 = npr9  if country == "nepal" & year == 2011
			cap replace other_v2 = lkr9  if country == "srilanka" & year == 2011
			*WP*
			cap replace other_v2 = khr12 if country == "cambodia" & year == 2010
			cap replace other_v2 = gur8  if country == "guam" & year == 2011
			cap replace other_v2 = hkr15 if country == "hongkong" & year == 2009
			cap replace other_v2 = kir11 if country == "kiribati" & year == 2009
			cap replace other_v2 = cr8   if country == "macau" & year == 2010
			cap replace other_v2 = cr8   if country == "malaysia" & year == 2009
			cap replace other_v2 = cr8   if country == "micronesia" & year == 2010
			cap replace other_v2 = cr8   if country == "mongolia" & year == 2007
			cap replace other_v2 = cr8   if country == "newcaledonia" & year == 2010
			cap replace other_v2 = phr8  if country == "philippines" & year >= 2007
			cap replace other_v2 = cr8   if country == "tonga" & year == 2010
			cap gen other_v3 = . /*smokeless tobacco*/
			*AFR*
			cap replace other_v3 = cr9   if region  == "AFR" & year >= 2008
			cap replace other_v3 = .     if region  == "AFR" & year >= 2008 & other_v1 != .
			cap replace other_v3 = cgr9  if country == "congo" & year == 2009
			cap replace other_v3 = cir9  if country == "cotedivoire" & year == 2009
			cap replace other_v3 = gnr9  if country == "guinea" & year == 2008
			cap replace other_v3 = mwr10 if country == "malawi" & year == 2009
			cap replace other_v3 = .     if country == "mali" & year == 2008
			cap replace other_v3 = .     if country == "mauritius" & year == 2008
			cap replace other_v3 = str9  if country == "saotomeandprincipe" & year == 2010
			cap replace other_v3 = cr9   if country == "seychelles" & year == 2007
			cap replace other_v3 = cr9   if country == "uganda" & year == 2007
			cap replace other_v3 = cr9   if country == "zambia" & year == 2007
			*EM*
			cap replace other_v3 = cr9   if region  == "EM" & year == 2008 & other_v1 != .
			cap replace other_v3 = djr9  if country == "djibouti" & year == 2009
			cap replace other_v3 = cr9   if country == "iran" & year == 2007
			cap replace other_v3 = cr9   if country == "qatar" & year == 2007
			cap replace other_v2 = cr9   if country == "tunisia" & year == 2007
			*ROTA*
			cap replace other_v3 = cr10  if region == "ROTA" & year >= 2009
			cap replace other_v3 = cr10  if country == "belize" & year == 2008
			cap replace other_v3 = svr9  if country == "elsalvador" & year == 2009
			cap replace other_v3 = cr9   if country == "panama" & year == 2008
			cap replace other_v3 = cr9   if country == "trinidadandtobago" & year == 2011
			*SEA*
			cap replace other_v3 = cr9   if country == "srilanka" & year == 2007
			cap replace other_v3 = thr9  if country == "thailand" & year == 2009
			cap replace other_v3 = btr15 if country == "bhutan" & year == 2009 & btr14 == 1
			cap replace other_v2 = cr9   if country == "easttimor" & year == 2009
			cap replace other_v3 = cr9   if country == "myanmar" & year == 2007
			cap replace other_v3 = npr4  if country == "nepal" & year < 2007
			cap replace other_v3 = cr9   if country == "nepal" & year == 2007
			*WP*
			cap replace other_v3 = khr13 if country == "cambodia" & year == 2010
			cap replace other_v3 = gur9  if country == "guam" & year == 2011
			cap replace other_v3 = kir12 if country == "kiribati" & year == 2009
			cap replace other_v3 = cr9   if country == "macau" & year == 2010
			cap replace other_v3 = cr9   if country == "malaysia" & year == 2009
			cap replace other_v3 = cr9   if country == "micronesia" & year == 2010
			cap replace other_v3 = cr9   if country == "mongolia" & year == 2007
			cap replace other_v3 = phr9  if country == "philippines" & year >= 2007
			cap replace other_v3 = cr9   if country == "southkorea" & year == 2008
			cap replace other_v3 = cr9   if country == "tonga" & year == 2010
			cap gen other_v4 = . /*cigars, mini cigars, cigarillos*/
			*EU*
			cap replace other_v4 = cr8   if region  == "EU" & year != 2002 & year != 1999
			cap replace other_v4 = .     if country == "czechrepublic"
			cap replace other_v4 = .     if country == "georgia" & year == 2008
			cap replace other_v4 = hur9  if country == "hungary" & year == 2008
			cap replace other_v4 = .     if country == "italy"
			cap replace other_v4 = ltr8  if country == "lithuania"
			cap replace other_v4 = .     if country == "lithuania" & year == 2009
			cap replace other_v4 = .     if country == "romania" & year == 2009
			cap replace other_v4 = .     if country == "sanmarino"
			cap replace other_v4 = uzr8  if country == "uzbekistan"
			cap gen other_v5 = . /*chew, snuff, dip*/
			*EU*
			cap replace other_v5 = cr9   if region  == "EU" & year != 2002 & year != 1999
			cap replace other_v5 = .     if country == "armenia" & year == 2009
			cap replace other_v5 = .     if country == "bulgaria" & year == 2008
			cap replace other_v5 = .     if country == "cyprus" & year == 2005
			cap replace other_v5 = .     if country == "czechrepublic"
			cap replace other_v5 = .     if country == "georgia" & year == 2008
			cap replace other_v5 = .     if country == "hungary" & year == 2003
			cap replace other_v5 = hur10 if country == "hungary" & year == 2008
			cap replace other_v5 = .     if country == "italy"
			cap replace other_v5 = kzr9  if country == "kazakhstan"
			cap replace other_v5 = ltr9  if country == "lithuania"
			cap replace other_v5 = .     if country == "lithuania" & year == 2009
			cap replace other_v5 = .     if country == "romania" & year == 2009
			cap replace other_v5 = .     if country == "sanmarino"
			cap replace other_v5 = .     if country == "slovakia" & year == 2003
			cap replace other_v5 = skr9  if country == "slovakia" & year != 2003
			cap replace other_v5 = .     if country == "uzbekistan"
			cap gen other_v6 = . /*pipe, nasal snuff*/
			*EU*
			cap replace other_v6 = cr10  if region  == "EU" & year != 2002 & year != 1999
			cap replace other_v6 = azr10 if country == "azerbaijan" & year ==2011
			cap replace other_v6 = .     if country == "czechrepublic"
			cap replace other_v6 = .     if country == "georgia" & year == 2008
			cap replace other_v6 = hur11 if country == "hungary" & year == 2008
			cap replace other_v6 = .     if country == "italy"
			cap replace other_v6 = .     if country == "latvia" & year == 2011
			cap replace other_v6 = .     if country == "lithuania" & year == 2009
			cap replace other_v6 = plr10 if country == "poland" & year == 2009
			cap replace other_v6 = .     if country == "romania" & year == 2009
			cap replace other_v6 = .     if country == "sanmarino"
			cap replace other_v6 = .     if country == "slovakia" & year != 2003
			cap replace other_v6 = sir10 if country == "slovenia" & year == 2011
			cap gen other_v7 = . /*regional types of tobacco*/
			*EU*
			cap replace other_v7 = amr9  if country == "armenia" & year == 2009
			cap replace other_v7 = kgr10 if country == "kyrgyzstan" & year == 2004
			cap replace other_v7 = plr10 if country == "poland" & year == 2003
			cap replace other_v7 = plr9  if country == "poland" & year == 2009
			cap replace other_v7 = tjr11 if country == "tajikistan" & year == 2004
		
		
			*** define PARENTS ***

			cap gen parents_v1 = . /*parents, smoke*/
			cap replace parents_v1 = cr14
			*AFR*
			cap replace parents_v1 = cvr22 if country == "capeverde"
			cap replace parents_v1 = cir14 if country == "cotedivoire" & year == 2003
			cap replace parents_v1 = ker16 if country == "kenya" & year == 2007
			cap replace parents_v1 = cr12  if country == "mauritania" & year == 2009
			cap replace parents_v1 = cr15  if country == "nigeria" & year == 2000
			cap replace parents_v1 = cr12  if country == "saotomeandprincipe"
			cap replace parents_v1 = cr12  if country == "southafrica" & year == 1999
			cap replace parents_v1 = szr17 if country == "swaziland" & year == 2001
			cap replace parents_v1 = ugr14 if country == "uganda" & year == 2002
			cap replace parents_v1 = cr12  if country == "zimbabwe" & year == 1999
			cap replace parents_v1 = cr12  if country == "botswana" & year == 2008
			cap replace parents_v1 = cr12  if country == "burkinafaso" & year == 2009
			cap replace parents_v1 = cr12  if country == "burundi" & year == 2008
			cap replace parents_v1 = cr12  if country == "cameroon" & year == 2008
			cap replace parents_v1 = cr12  if country == "cenafricanrep" & year == 2008
			cap replace parents_v1 = cr12  if country == "congo" & year == 2009
			cap replace parents_v1 = cr12  if country == "cotedivoire" & year == 2009
			cap replace parents_v1 = cr12  if country == "demrepcongo" & year == 2008
			cap replace parents_v1 = cr12  if country == "equatorialguinea" & year == 2008
			cap replace parents_v1 = cr12  if country == "gambia" & year == 2008
			cap replace parents_v1 = cr12  if country == "ghana" & year == 2009
			cap replace parents_v1 = cr12  if country == "ghana" & year == 2008
			cap replace parents_v1 = cr12  if country == "guinea" & year == 2008
			cap replace parents_v1 = cr12  if country == "guineabissau" & year == 2008
			cap replace parents_v1 = cr12  if country == "liberia" & year == 2008
			cap replace parents_v1 = cr12  if country == "madagascar" & year == 2008
			cap replace parents_v1 = cr12  if country == "malawi" & year == 2009
			cap replace parents_v1 = cr12  if country == "mali" & year == 2008
			cap replace parents_v1 = cr12  if country == "mauritius" & year == 2008
			cap replace parents_v1 = cr12  if country == "namibia" & year == 2008
			cap replace parents_v1 = cr12  if country == "nigeria" & year == 2008
			cap replace parents_v1 = cr12  if country == "niger" & year == 2009
			cap replace parents_v1 = cr12  if country == "seychelles" & year == 2007
			cap replace parents_v1 = cr12  if country == "sierraleone" & year == 2008
			cap replace parents_v1 = cr12  if country == "southafrica" & year == 2008
			cap replace parents_v1 = cr12  if country == "swaziland" & year == 2009
			cap replace parents_v1 = cr12  if country == "tanzania" & year == 2008
			cap replace parents_v1 = cr12  if country == "uganda" & year == 2007
			cap replace parents_v1 = cr12  if country == "uganda" & year == 2011
			cap replace parents_v1 = cr12  if country == "uganda" & year == 2007
			cap replace parents_v1 = cr12  if country == "zambia" & year == 2007
			cap replace parents_v1 = cr12  if country == "zambia" & year == 2011
			cap replace parents_v1 = cr12  if country == "zimbabwe" & year == 1999
			cap replace parents_v1 = cr12  if country == "zimbabwe" & year == 2008
			cap replace parents_v1 = cr15  if country == "ghana" & year == 2000
			cap replace parents_v1 = cr15  if country == "malawi" & year == 2000
			cap replace parents_v1 = lsr16 if country == "lesotho" & year == 2008
			cap replace parents_v1 = .     if country == "rwanda" & year == 2008
			cap replace parents_v1 = zar35 if country == "southafrica" & year == 2011
			*EM*
			cap replace parents_v1 = egr14 if country == "egypt" & year < 2009
			cap replace parents_v1 = cr12  if country == "jordan" & year == 1999
			cap replace parents_v1 = cr12  if country == "gazastrip" & year == 2008
			cap replace parents_v1 = cr12  if country == "iran" & year == 2007
			cap replace parents_v1 = cr12  if country == "iraq" & year == 2008
			cap replace parents_v1 = cr12  if country == "jordan" & year == 2008
			cap replace parents_v1 = cr12  if country == "lebanon" & year == 2011
			cap replace parents_v1 = cr12  if country == "lebanon" & year == 2008
			cap replace parents_v1 = cr12  if country == "pakistan" & year == 2008
			cap replace parents_v1 = cr12  if country == "qatar" & year == 2007
			cap replace parents_v1 = cr12  if country == "syria" & year == 2007
			cap replace parents_v1 = cr12  if country == "syria" & year == 2008
			cap replace parents_v1 = cr12  if country == "tunisia" & year == 2007
			cap replace parents_v1 = cr12  if country == "westbank" & year == 2008
			cap replace parents_v1 = cr12  if country == "yemen" & year == 2008
			cap replace parents_v1 = pbr19 if country == "gazastrip" & year == 2000
			cap replace parents_v1 = pbr19 if country == "westbank" & year == 2000
			*EU*
			cap replace parents_v1 = cr20  if country == "albania" & year == 2004
			cap replace parents_v1 = cr20  if country == "armenia" & year == 2004
			cap replace parents_v1 = cr20  if country == "belarus"
			cap replace parents_v1 = cr20  if country == "bosniaherzegovina" & year == 2003
			cap replace parents_v1 = cr20  if country == "croatia" & year < 2011
			cap replace parents_v1 = cr20  if country == "cyprus"		
			cap replace parents_v1 = cr20  if country == "estonia"
			cap replace parents_v1 = cr20  if country == "greece"
			cap replace parents_v1 = cr20  if country == "georgia" & year == 2003
			cap replace parents_v1 = cr20  if country == "hungary" & year == 2003
			cap replace parents_v1 = cr20  if country == "kazakhstan" & year == 2004
			cap replace parents_v1 = kor20 if country == "kosovo"
			cap replace parents_v1 = cr20  if country == "kyrgyzstan" & year == 2004
			cap replace parents_v1 = lv21  if country == "latvia" & year == 2007
			cap replace parents_v1 = cr20  if country == "macedonia" & year == 2003
			cap replace parents_v1 = cr20  if country == "moldova" & year == 2004
			cap replace parents_v1 = cr20  if country == "montenegro"
			cap replace parents_v1 = cr12  if country == "poland" & year == 1999
			cap replace parents_v1 = cr20  if country == "poland" & year == 2003
			cap replace parents_v1 = cr20  if country == "romania" & year == 2004
			cap replace parents_v1 = cr12  if country == "russianfederation" & year == 1999
			cap replace parents_v1 = cr20  if country == "russianfederation" & year == 2004
			cap replace parents_v1 = cr20  if country == "slovakia" & year < 2011
			cap replace parents_v1 = cr20  if country == "slovenia" & year < 2011
			cap replace parents_v1 = cr20  if country == "tajikistan"
			cap replace parents_v1 = cr20  if country == "turkey"
			cap replace parents_v1 = cr20  if country == "ukraine" & year == 2005
			cap replace parents_v1 = cr12  if country == "ukraine" & year == 1999
			cap replace parents_v1 = cr16  if country == "albania" & year == 2009
			cap replace parents_v1 = cr16  if country == "armenia" & year == 2009
			cap replace parents_v1 = cr16  if country == "azerbaijan" & year == 2011
			cap replace parents_v1 = cr16  if country == "bosniaherzegovina" & year == 2008
			cap replace parents_v1 = cr16  if country == "bulgaria" & year == 2008
			cap replace parents_v1 = cr16  if country == "croatia" & year == 2011
			cap replace parents_v1 = cr16  if country == "czechrepublic" & year == 2011
			cap replace parents_v1 = cr16  if country == "georgia" & year == 2008
			cap replace parents_v1 = cr16  if country == "italy" & year == 2010
			cap replace parents_v1 = cr16  if country == "kazakhstan" & year == 2009
			cap replace parents_v1 = cr16  if country == "kyrgyzstan" & year == 2008
			cap replace parents_v1 = cr16  if country == "latvia" & year == 2011
			cap replace parents_v1 = cr16  if country == "macedonia" & year == 2008
			cap replace parents_v1 = cr16  if country == "moldova" & year == 2008
			cap replace parents_v1 = cr16  if country == "poland" & year == 2009
			cap replace parents_v1 = cr16  if country == "romania" & year == 2009
			cap replace parents_v1 = cr16  if country == "sanmarino" & year == 2010
			cap replace parents_v1 = cr16  if country == "serbia" & year == 2008
			cap replace parents_v1 = cr16  if country == "slovakia" & year == 2011
			cap replace parents_v1 = cr16  if country == "slovenia" & year == 2011
			cap replace parents_v1 = cr16  if country == "ukraine" & year == 2011
			cap replace parents_v1 = cr16  if country == "uzbekistan" & year == 2008
			cap replace parents_v1 = cr20  if country == "poland" & year == 2003
			cap replace parents_v1 = ltr14 if country == "lithuania" & year == 2009
			*ROTA*
			cap replace parents_v1 = cr15  if country == "argentina"
			cap replace parents_v1 = cr13  if country == "argentina" 7 year == 2007
			cap replace parents_v1 = brr22 if country == "brazil" & year == 2005
			cap replace parents_v1 = brr22 if country == "brazil" & year == 2006
			cap replace parents_v1 = brr22 if country == "brazil" & year == 2007
			cap replace parents_v1 = cr15  if country == "chile" & year == 2000
			cap replace parents_v1 = cr12  if country == "costarica" & year == 1999
			cap replace parents_v1 = gyr18 if country == "guyana" & year == 2004
			cap replace parents_v1 = cr15  if country == "mexico" & city == "monterrey" & year == 2000
			cap replace parents_v1 = cr15  if country == "peru" & year == 2000
			cap replace parents_v1 = cr15  if country == "uruguay"
			cap replace parents_v1 = cr14  if country == "uruguay" & year == 2007
			cap replace parents_v1 = cr12  if country == "venezuela" & year == 1999
			cap replace parents_v1 = .     if country == "venezuela" & year == 2010
			cap replace parents_v1 = brr22 if country == "brazil" & year == 2006
			cap replace parents_v1 = bsr15 if country == "bahamas" & year == 2000
			cap replace parents_v1 = cr12  if country == "barbados" & year == 1999
			cap replace parents_v1 = cr12  if country == "trinidadandtobago" & year == 2011
			cap replace parents_v1 = cr13  if country == "antiguaandbarbuda" & year == 2009
			cap replace parents_v1 = cr13  if country == "barbados" & year == 2007
			cap replace parents_v1 = cr13  if country == "belize" & year == 2008
			cap replace parents_v1 = cr13  if country == "chile" & year == 2008
			cap replace parents_v1 = cr13  if country == "colombia" & year == 2007
			cap replace parents_v1 = cr13  if country == "costarica" & year == 2008
			cap replace parents_v1 = cr13  if country == "cuba" & year == 2010
			cap replace parents_v1 = cr13  if country == "dominica" & year == 2009
			cap replace parents_v1 = cr13  if country == "ecuador" & year == 2007
			cap replace parents_v1 = cr13  if country == "ecuador" & year == 2007
			cap replace parents_v1 = cr13  if country == "ecuador" & year == 2007
			cap replace parents_v1 = cr13  if country == "elsalvador" & year == 2009
			cap replace parents_v1 = cr13  if country == "grenada" & year == 2008
			cap replace parents_v1 = cr13  if country == "guatemala" & year == 2008
			cap replace parents_v1 = cr13  if country == "guyana" & year == 2010
			cap replace parents_v1 = cr13  if country == "jamaica" & year == 2010
			cap replace parents_v1 = cr13  if country == "mexico" & year == 2011					
			cap replace parents_v1 = cr13  if country == "panama" & year == 2008
			cap replace parents_v1 = cr13  if country == "paraguay" & year == 2008
			cap replace parents_v1 = cr13  if country == "peru" & year == 2007					
			cap replace parents_v1 = cr13  if country == "saintkittsandnevis" & year == 2010
			cap replace parents_v1 = cr13  if country == "saintvincent" & year == 2011
			cap replace parents_v1 = cr13  if country == "suriname" & year == 2009
			cap replace parents_v1 = cr13  if country == "venezuela" & year == 2008
			cap replace parents_v1 = cr15  if country == "antiguaandbarbuda" & year == 2000
			cap replace parents_v1 = cr15  if country == "bolivia" & year == 2000
			cap replace parents_v1 = cr15  if country == "cuba" & year == 2000
			cap replace parents_v1 = cr15  if country == "dominica" & year == 2000
			cap replace parents_v1 = cr15  if country == "grenada" & year == 2000
			cap replace parents_v1 = cr13  if country == "grenada" & year == 2009
			cap replace parents_v1 = cr15  if country == "haiti" & year == 2000
			cap replace parents_v1 = cr15  if country == "montserrat" & year == 2000
			cap replace parents_v1 = cr15  if country == "saintvincent" & year == 2000
			cap replace parents_v1 = cr15  if country == "suriname" & year == 2000
			cap replace parents_v1 = cr15  if country == "trinidadandtobago" & year == 2000
			cap replace parents_v1 = gyr18 if country == "guyana" & year == 2000
			cap replace parents_v1 = lcr13 if country == "saintlucia" & year == 2011
			cap replace parents_v1 = lcr19 if country == "saintlucia" & year == 2000
			cap replace parents_v1 = .     if country == "jamaica" & year == 2000
			*SEA*
			cap replace parents_v1 = inr27 if country == "bangladesh" & year == 2004
			cap replace parents_v1 = cr12  if country == "bangladesh" & year == 2007
			cap replace parents_v1 = inr27 if country == "india" & city != "natl"
			cap replace parents_v1 = inr28 if country == "india" & city == "westbengal"
			cap replace parents_v1 = cr12  if country == "india" & city == "natl" & year == 2009
			cap replace parents_v1 = cr14  if country == "india" & city == "natl" & year == 2006
			cap replace parents_v1 = cr15  if country == "indonesia" & year == 2000
			cap replace parents_v1 = mmr19 if country == "myanmar" & year == 2004
			cap replace parents_v1 = cr12  if country == "myanmar" & year == 2007
			cap replace parents_v1 = cr15  if country == "srilanka" & year == 1999
			cap replace parents_v1 = cr12  if country == "bhutan" & year == 2009
			cap replace parents_v1 = cr12  if country == "easttimor" & year == 2009
			cap replace parents_v1 = cr12  if country == "indonesia" & year == 2009
			cap replace parents_v1 = cr12  if country == "maldives" & year == 2007
			cap replace parents_v1 = cr12  if country == "nepal" & year == 2007
			cap replace parents_v1 = cr12  if country == "srilanka" & year == 2007
			cap replace parents_v1 = cr12  if country == "thailand" & year == 2009
			cap replace parents_v1 = mmr20 if country == "myanmar" & year == 2001
			cap replace parents_v1 = npr26 if country == "nepal" & year == 2001
			*WP*
			cap replace parents_v1 = cr12  if country == "china" & year == 1999
			cap replace parents_v1 = nzr11 if country == "newzealand" & year < 2010
			cap replace parents_v1 = nzr10 if country == "newzealand" & year == 2010
			cap replace parents_v1 = cr15  if country == "philippines" & year == 2000
			cap replace parents_v1 = cr15  if country == "singapore"
			cap replace parents_v1 = cr12  if country == "cookislands" & year == 2008
			cap replace parents_v1 = cr12  if country == "fiji" & year == 1999
			cap replace parents_v1 = cr12  if country == "fiji" & year == 2009
			cap replace parents_v1 = cr12  if country == "hongkong" & year == 2009
			cap replace parents_v1 = cr12  if country == "kiribati" & year == 2009
			cap replace parents_v1 = cr12  if country == "laos" & year == 2011
			cap replace parents_v1 = cr12  if country == "laos" & year == 2007
			cap replace parents_v1 = cr12  if country == "macau" & year == 2010
			cap replace parents_v1 = cr12  if country == "malaysia" & year == 2009
			cap replace parents_v1 = cr12  if country == "marshallislands" & year == 2009
			cap replace parents_v1 = cr12  if country == "mongolia" & year == 2007
			cap replace parents_v1 = cr12  if country == "newcaledonia" & year == 2010
			cap replace parents_v1 = cr12  if country == "niue" & year == 2009
			cap replace parents_v1 = cr12  if country == "southkorea" & year == 2008
			cap replace parents_v1 = cr12  if country == "tonga" & year == 2010
			cap replace parents_v1 = cr12  if country == "vietnam" & year == 2007
			cap replace parents_v1 = cr12  if country == "vietnam" & year == 2007
			cap replace parents_v1 = sbr20 if country == "solomonislands" & year == 2008
			cap gen parents_v2 = ./*parents, tobacco*/
			*SEA*
			cap replace parents_v2 = inr26 if country == "india" & city == "natl"
			cap replace parents_v2 = npr26 if country == "nepal" & year <= 2004
			cap gen parents_v3 = . /*female guardian, smoke*/
			*SEA*
			cap replace parents_v3 = hur23 if country == "hungary" & year == 2008
			cap gen parents_v4 = . /*male guardian, smoke*/
			*SEA*
			cap replace parents_v4 = hur24 if country == "hungary" & year == 2008
			cap gen parents_v5 = . /*parents,narguileh*/
			*EM*
			cap replace parents_v5 = lbr20 if country == "pakistan" & year == 2003

			*** define COMFORT ***

			cap gen comfort_v1 = . /*cigarettes, comfortable*/
			cap replace comfort_v1 = cr22
			*AFR*
			cap replace comfort_v1 = cr20  if country == "saotomeandprincipe"
			cap replace comfort_v1 = .     if country == "egypt" & year == 2001
			cap replace comfort_v1 = egr22 if country == "egypt" & year == 2005
			cap replace comfort_v1 = cr18  if country == "egypt" & year == 2009
			cap replace comfort_v1 = cr20  if country == "jordan" & year == 1999
			cap replace comfort_v1 = .     if country == "morocco" & year < 2010
			cap replace comfort_v1 = mar23 if country == "morocco" & year == 2010
			cap replace comfort_v1 = cr23  if country == "nigeria" & year == 2000
			cap replace comfort_v1 = cr20  if country == "nigeria" & year == 2008
			cap replace comfort_v1 = cr20  if country == "southafrica" & year == 1999
			cap replace comfort_v1 = sar23 if country == "saudiarabia" & year == 2001
			cap replace comfort_v1 = sar22 if country == "saudiarabia" & year == 2007
			cap replace comfort_v1 = cr20  if country == "zimbabwe" & year == 1999
			cap replace comfort_v1 = cr20  if country == "botswana" & year == 2009
			cap replace comfort_v1 = cr20  if country == "burkinafaso" & year == 2009		
			cap replace comfort_v1 = cr20  if country == "burundi" & year == 2008
			cap replace comfort_v1 = cr20  if country == "cameroon" & year == 2008				
			cap replace comfort_v1 = cr20  if country == "cenafricanrep" & year == 2008
			cap replace comfort_v1 = cr20  if country == "congo" & year == 2009
			cap replace comfort_v1 = cr20  if country == "cotedivoire" & year == 2009
			cap replace comfort_v1 = cr20  if country == "demrepcongo" & year == 2008
			cap replace comfort_v1 = cr20  if country == "equatorialguinea" & year == 2008
			cap replace comfort_v1 = cr20  if country == "gambia" & year == 2008
			cap replace comfort_v1 = cr20  if country == "ghana" & year == 2009
			cap replace comfort_v1 = cr20  if country == "guineabissau" & year == 2008
			cap replace comfort_v1 = cr20  if country == "guinea" & year == 2008
			cap replace comfort_v1 = cr20  if country == "lesotho" & year == 2008
			cap replace comfort_v1 = cr20  if country == "liberia" & year == 2008
			cap replace comfort_v1 = cr20  if country == "madagascar" & year == 2008
			cap replace comfort_v1 = cr20  if country == "malawi" & year == 2009
			cap replace comfort_v1 = cr20  if country == "mali" & year == 2008
			cap replace comfort_v1 = cr20  if country == "mauritania" & year == 2009
			cap replace comfort_v1 = cr20  if country == "mauritius" & year == 2008
			cap replace comfort_v1 = cr20  if country == "namibia" & year == 2008
			cap replace comfort_v1 = cr20  if country == "niger" & year == 2009
			cap replace comfort_v1 = cr20  if country == "rwanda" & year == 2008
			cap replace comfort_v1 = cr20  if country == "seychelles" & year == 2007
			cap replace comfort_v1 = cr20  if country == "sierraleone" & year == 2008
			cap replace comfort_v1 = cr20  if country == "southafrica" & year == 2008
			cap replace comfort_v1 = cr20  if country == "southafrica" & year == 2011
			cap replace comfort_v1 = cr20  if country == "swaziland" & year == 2009
			cap replace comfort_v1 = cr20  if country == "tanzania" & year == 2008
			cap replace comfort_v1 = cr20  if country == "uganda" & year == 2007
			cap replace comfort_v1 = cr20  if country == "uganda" & year == 2011
			cap replace comfort_v1 = cr20  if country == "zambia" & year == 2011
			cap replace comfort_v1 = cr20  if country == "zambia" & year == 2007			
			cap replace comfort_v1 = cr23  if country == "ghana" & year == 2000
			cap replace comfort_v1 = cr23  if country == "malawi" & year == 2000
			*EM*
			cap replace comfort_v1 = cr18  if country == "saudiarabia" & year == 2010
			cap replace comfort_v1 = sdr33 if country == "sudan" & year == 2005
			cap replace comfort_v1 = tnr23 if country == "tunisia" & year == 2001
			cap replace comfort_v1 = .     if country == "pakistan" & year == 2003
			cap replace comfort_v1 = cr18  if country == "djibouti" & year == 2009
			cap replace comfort_v1 = cr18  if country == "jordan" & year == 2009
			cap replace comfort_v1 = cr18  if country == "kuwait" & year == 2009
			cap replace comfort_v1 = cr18  if country == "libya" & year == 2010
			cap replace comfort_v1 = cr18  if country == "sudan" & year == 2009
			cap replace comfort_v1 = cr18  if country == "syria" & year == 2010
			cap replace comfort_v1 = cr18  if country == "tunisia" & year == 2010
			cap replace comfort_v1 = cr18  if country == "westbank" & year == 2009
			cap replace comfort_v1 = cr20  if country == "gazastrip" & year == 2008
			cap replace comfort_v1 = cr20  if country == "iran" & year == 2007
			cap replace comfort_v1 = cr20  if country == "iraq" & year == 2008
			cap replace comfort_v1 = cr20  if country == "jordan" & year == 1999
			cap replace comfort_v1 = cr20  if country == "jordan" & year == 2008
			cap replace comfort_v1 = cr20  if country == "lebanon" & year == 2011
			cap replace comfort_v1 = cr20  if country == "lebanon" & year == 2008
			cap replace comfort_v1 = cr20  if country == "pakistan" & year == 2008
			cap replace comfort_v1 = cr20  if country == "qatar" & year == 2027
			cap replace comfort_v1 = cr20  if country == "syria" & year == 2007
			cap replace comfort_v1 = cr20  if country == "syria" & year == 2008
			cap replace comfort_v1 = cr20  if country == "tunisia" & year == 2007
			cap replace comfort_v1 = cr20  if country == "westbank" & year == 2008
			cap replace comfort_v1 = cr20  if country == "yemen" & year == 2008
			cap replace comfort_v1 = .     if country == "gazastrip" & year == 2000
			cap replace comfort_v1 = .     if country == "westbank" & year == 2000
			cap replace comfort_v1 = omr28 if country == "oman" & year == 2010
			cap replace comfort_v1 = sar23 if country == "saudiarabia" & year == 2001
			*EU*
			cap replace comfort_v1 = cr26  if country == "bosniaherzegovina" & city == "srpska"
			cap replace comfort_v1 = cr26  if country == "croatia" & year < 2011
			cap replace comfort_v1 = cr22  if country == "croatia" & year == 2011
			cap replace comfort_v1 = cr26  if country == "greece"
			cap replace comfort_v1 = cr26  if country == "hungary" & year == 2003
			cap replace comfort_v1 = hur31 if country == "hungary" & year == 2008
			cap replace comfort_v1 = cr26  if country == "kazakhstan" & year == 2004
			cap replace comfort_v1 = cr22  if country == "kazakhstan" & year == 2009
			cap replace comfort_v1 = lvr27 if country == "latvia" & year == 2002
			cap replace comfort_v1 = cr26  if country == "latvia" & year == 2007
			cap replace comfort_v1 = cr20  if country == "poland" & year == 1999
			cap replace comfort_v1 = cr26  if country == "poland" & year == 2003
			cap replace comfort_v1 = mkr26 if country == "macedonia" & year == 2003
			cap replace comfort_v1 = .     if country == "macedonia" & year == 2008
			cap replace comfort_v1 = cr26  if country == "romania" & year == 2004
			cap replace comfort_v1 = cr22  if country == "romania" & year == 2009
			cap replace comfort_v1 = cr20  if country == "russianfederation" & year == 1999
			cap replace comfort_v1 = cr26  if country == "russianfederation" & year == 2004
			cap replace comfort_v1 = cr26  if country == "turkey"
			cap replace comfort_v1 = cr20  if country == "ukraine" & year == 1999
			cap replace comfort_v1 = cr26  if country == "ukraine" & year == 2005
			cap replace comfort_v1 = cr22  if country == "ukraine" & year == 2011
			cap replace comfort_v1 = cr26  if country == "albania" & year == 2004
			cap replace comfort_v1 = cr26  if country == "armenia" & year == 2004
			cap replace comfort_v1 = cr26  if country == "belarus" & year == 2004
			cap replace comfort_v1 = cr26  if country == "bosniaherzegovina" & year == 2003
			cap replace comfort_v1 = cr26  if country == "cyprus" & year == 2005
			cap replace comfort_v1 = cr26  if country == "estonia" & year == 2003
			cap replace comfort_v1 = cr26  if country == "estonia" & year == 2007
			cap replace comfort_v1 = cr26  if country == "georgia" & year == 2003
			cap replace comfort_v1 = cr26  if country == "kosovo" & year == 2004
			cap replace comfort_v1 = cr26  if country == "kyrgyzstan" & year == 2004
			cap replace comfort_v1 = cr26  if country == "moldova" & year == 2004
			cap replace comfort_v1 = cr26  if country == "montenegro" & year == 2004
			cap replace comfort_v1 = cr26  if country == "poland" & year == 2003
			cap replace comfort_v1 = cr26  if country == "slovakia" & year < 2011
			cap replace comfort_v1 = cr22  if country == "slovakia" & year == 2011
			cap replace comfort_v1 = cr26  if country == "slovenia"	& year < 2011
			cap replace comfort_v1 = cr22  if country == "slovenia"	& year == 2011
			*ROTA*
			cap replace comfort_v1 = cr23  if country == "argentina" & year == 2000
			cap replace comfort_v1 = cr21  if country == "argentina" & year == 2007
			cap replace comfort_v1 = cr23  if country == "chile" & year == 2000
			cap replace comfort_v1 = cr23  if country == "colombia" & year == 2000
			cap replace comfort_v1 = cr20  if country == "costarica" & year == 1999
			cap replace comfort_v1 = dmr24 if country == "dominica" & year == 2000
			cap replace comfort_v1 = cr23  if country == "mexico" & city == "monterrey" & year == 2000
			cap replace comfort_v1 = cr23  if country == "peru" & year == 2000
			cap replace comfort_v1 = cr20  if country == "venezuela" & year == 1999
			cap replace comfort_v1 = .     if country == "venezuela" & year == 2010
			cap replace comfort_v1 = cr23  if country == "uruguay" if year == 2000
			cap replace comfort_v1 = cr23  if country == "uruguay" if year == 2007
			cap replace comfort_v1 = cor26 if country == "colombia" & year == 2001
			cap replace comfort_v1 = cr20  if country == "barbados" & year == 1999
			cap replace comfort_v1 = cr20  if country == "trinidadandtobago" & year == 2011
			cap replace comfort_v1 = cr21  if country == "antiguaandbarbuda" & year == 2009
			cap replace comfort_v1 = cr21  if country == "argentina" & year == 2007
			cap replace comfort_v1 = cr21  if country == "barbados" & year == 2007
			cap replace comfort_v1 = cr21  if country == "belize" & year == 2008
			cap replace comfort_v1 = cr21  if country == "chile" & year == 2008
			cap replace comfort_v1 = cr21  if country == "colombia" & year == 2007
			cap replace comfort_v1 = cr21  if country == "costarica" & year == 2008
			cap replace comfort_v1 = cr21  if country == "cuba" & year == 2010
			cap replace comfort_v1 = cr21  if country == "dominica" & year == 2009
			cap replace comfort_v1 = cr21  if country == "ecuador" & year == 2007
			cap replace comfort_v1 = cr21  if country == "elsalvador" & year == 2009
			cap replace comfort_v1 = cr21  if country == "grenada" & year == 2009
			cap replace comfort_v1 = cr21  if country == "guatemala" & year == 2008
			cap replace comfort_v1 = cr21  if country == "guyana" & year == 2010
			cap replace comfort_v1 = cr21  if country == "jamaica" & year == 2010
			cap replace comfort_v1 = cr21  if country == "mexico" & year == 2011
			cap replace comfort_v1 = cr21  if country == "panama" & year == 2008
			cap replace comfort_v1 = cr21  if country == "paraguay" & year == 2008
			cap replace comfort_v1 = cr21  if country == "peru" & year == 2007
			cap replace comfort_v1 = cr21  if country == "saintkittsandnevis" & year == 2010
			cap replace comfort_v1 = cr21  if country == "saintlucia" & year == 2011
			cap replace comfort_v1 = cr21  if country == "saintvincent" & year == 2011
			cap replace comfort_v1 = cr21  if country == "suriname" & year == 2009
			cap replace comfort_v1 = cr21  if country == "venezuela" & year == 2008
			cap replace comfort_v1 = cr23  if country == "antiguaandbarbuda" & year == 2000
			cap replace comfort_v1 = cr23  if country == "bahamas" & year == 2000
			cap replace comfort_v1 = cr23  if country == "bolivia" & year == 2000
			cap replace comfort_v1 = cr23  if country == "cuba" & year == 2000
			cap replace comfort_v1 = cr23  if country == "grenada" & year == 2000
			cap replace comfort_v1 = cr23  if country == "guyana" & year == 2000
			cap replace comfort_v1 = cr23  if country == "haiti" & year == 2000
			cap replace comfort_v1 = cr23  if country == "jamaica" & year == 2000
			cap replace comfort_v1 = cr23  if country == "montserrat" & year == 2000
			cap replace comfort_v1 = cr23  if country == "saintlucia" & year == 2000
			cap replace comfort_v1 = cr23  if country == "saintvincent" & year == 2000
			cap replace comfort_v1 = cr23  if country == "suriname" & year == 2000
			cap replace comfort_v1 = cr23  if country == "trinidadandtobago" & year == 2000
			*SEA*
			cap replace comfort_v1 = inr35 if country == "bangladesh" & year == 2004
			cap replace comfort_v1 = cr20  if country == "bangladesh" & year == 2007
			cap replace comfort_v1 = inr43 if country == "india" & city == "westbengal"
			cap replace comfort_v1 = cr22  if country == "indonesia" & year == 2004
			cap replace comfort_v1 = cr22  if country == "indonesia" & year == 2005
			cap replace comfort_v1 = cr22  if country == "indonesia" & year == 2006
			cap replace comfort_v1 = cr23  if country == "indonesia" & year == 2000
			cap replace comfort_v1 = idr20 if country == "indonesia" & year == 2009
			cap replace comfort_v1 = cr20  if country == "myanmar" & year == 2007
			cap replace comfort_v1 = cr22  if country == "myanmar" & year == 2011
			cap replace comfort_v1 = npr41 if country == "nepal" & year == 2001
			cap replace comfort_v1 = npr41 if country == "nepal" & year == 2003
			cap replace comfort_v1 = npr41 if country == "nepal" & year == 2004
			cap replace comfort_v1 = cr20  if country == "nepal" & year == 2007
			cap replace comfort_v1 = cr22  if country == "nepal" & year == 2011
			cap replace comfort_v1 = cr23  if country == "srilanka" & year == 1999
			cap replace comfort_v1 = cr20  if country == "srilanka" & year == 2007
			cap replace comfort_v1 = cr20  if country == "bhutan" & year == 2009
			cap replace comfort_v1 = cr20  if country == "easttimor" & year == 2009
			cap replace comfort_v1 = cr20  if country == "india" & year == 2009
			cap replace comfort_v1 = cr20  if country == "maldives" & year == 2007
			cap replace comfort_v1 = cr20  if country == "thailand" & year == 2009
			cap replace comfort_v1 = inr35 if country == "india" & year == 2004
			cap replace comfort_v1 = inr35 if country == "india" & year == 2001
			cap replace comfort_v1 = inr35 if country == "india" & year == 2000
			cap replace comfort_v1 = inr35 if country == "india" & year == 2003	
			cap replace comfort_v1 = inr35 if country == "india" & year == 2002			
			cap replace comfort_v1 = mmr25 if country == "myanmar" & year == 2004
			cap replace comfort_v1 = mmr30 if country == "myanmar" & year == 2001
			*WP*
			cap replace comfort_v1 = cr20  if country == "china" & year == 1999
			cap replace comfort_v1 = .     if country == "kiribati"
			cap replace comfort_v1 = .     if country == "newzealand"
			cap replace comfort_v1 = cr23  if country == "philippines" & year == 2000
			cap replace comfort_v1 = cr23  if country == "singapore"
			cap replace comfort_v1 = sbr28 if country == "solomonislands"
			cap replace comfort_v1 = cr20  if country == "cookislands" & year == 2008
			cap replace comfort_v1 = cr20  if country == "fiji" & year == 1999
			cap replace comfort_v1 = cr20  if country == "fiji" & year == 2009
			cap replace comfort_v1 = cr20  if country == "hongkong" & year == 2009
			cap replace comfort_v1 = cr20  if country == "laos" & year == 2011
			cap replace comfort_v1 = cr20  if country == "laos" & year == 2007		
			cap replace comfort_v1 = cr20  if country == "macau" & year == 2010
			cap replace comfort_v1 = cr20  if country == "malaysia" & year == 2009
			cap replace comfort_v1 = cr20  if country == "marshallislands" & year == 2009
			cap replace comfort_v1 = cr20  if country == "mongolia" & year == 2007
			cap replace comfort_v1 = cr20  if country == "newcaledonia" & year == 2010
			cap replace comfort_v1 = cr20  if country == "niue" & year == 2009
			cap replace comfort_v1 = cr20  if country == "southkorea" & year == 2008
			cap replace comfort_v1 = cr20  if country == "tonga" & year == 2010
			cap replace comfort_v1 = cr20  if country == "vietnam" & year == 2007
			cap gen comfort_v2 = . /*tobacco, comfortable*/
			*SEA*
			cap replace comfort_v2 = inr35 if country == "india" & city != "natl" & year < 2006
			cap replace comfort_v2 = inr44 if country == "india" & city == "westbengal"
			cap replace comfort_v2 = npr41 if country == "nepal" & year == 2003
			cap replace comfort_v2 = npr42 if country == "nepal" & year == 2004
			cap replace comfort_v2 = mmr30 if country == "myanmar" & year == 2001
			cap replace comfort_v2 = mmr25 if country == "myanmar" & year == 2004
			cap gen comfort_v3 = . /*cigarettes, cool*/
			*ROTA*
			cap replace comfort_v3 = cor26 if country == "colombia" & year == 2001

			cap tempfile `i'_`j'
			cap save ``i'_`j'', replace
		}
	}
	clear
	gen drop = 1
	foreach i in ${`r'} {
		forvalues j = 1999/2011 {
			cap append using ``i'_`j''
		}
	}
	drop drop 
	order year country city region
	save `r', replace
}


*CHOOSE VARIABLES TO KEEP*
foreach r in AFR EM EU ROTA SEA WP {
	clear
	use `r'
	keep year country city region try* tryold* smokedays* cigperday* pocketid nobuy* other* parents* comfort* stratum psu
	save `r', replace
	}

*APPEND
clear
use AFR
foreach r in EM EU ROTA SEA WP {
	append using `r'
}
compress

***********************
*** add EIU prices to raw GYTS data:
***********************
/*
gen eiucity = city
replace eiucity = "natl" if country == "brazil" & city != "riodejaneiro"
replace eiucity = "natl" if country == "chile" & city != "santiago"
replace eiucity = "natl" if city == "chongqing" | city == "guangdong" | city == "shandong" | city == "macau" | city == "puyang" | city == "zhuhai"
replace eiucity = "natl" if country == "equador" & city != "quito"
replace eiucity = "natl" if country == "guatemala" & city != "guatemalacity"
replace eiucity = "mumbai" if country == "india" & city == "maharashtra"
replace eiucity = "newdelhi" if country == "india" & city == "delhi"
replace eiucity = "natl" if country == "india" & city != "mumbai" & city != "newdelhi"
replace eiucity = "natl" if country == "indonesia" & city != "jakarta"
replace eiucity = "natl" if country == "cotedivoire" & city != "abidjan"
replace eiucity = "natl" if country == "mexico" & city != "mexicocity"
replace eiucity = "natl" if country == "pakistan" | country == "poland" | country == "kazakhstan" | country == "nepal" | country == "ukraine" | country == "venezuela"
replace eiucity = "natl" if country == "paraguay" & city != "asuncion"
replace eiucity = "natl" if country == "peru" & city != "lima"
replace eiucity = "natl" if country == "russianfederation" & city != "moscow"
replace eiucity = "natl" if country == "uruguay" & city != "montevideo"
replace eiucity = "natl" if country == "vietnam" & city != "hanoi" & city != "hochiminh"
replace eiucity = "natl" if country == "zimbabwe" & city != "harare"
sort country eiucity year
merge country eiucity year using `prices'
tab _merge
keep if _merge == 3
drop _merge
sort country city eiucity year
*/

gen uniqid = _n
save "I:\group\TCORS-P50\Data\GYTS\Data\rawdata_combined_1", replace
log close
