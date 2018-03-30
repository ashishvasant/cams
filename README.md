# cams
%     first get the userinputs regarding the displacement time graph
prompt = {"maximum rise", "Start of rise", "End of rise", "Start of fall","End of fall"};
defaults = {"5","60", "120", "270","360"};
rowscols = [1,5;1,10; 2,20; 3,30; 4,40];
dim= inputdlg (prompt, "Enter displacement diagram characteristics", rowscols, defaults);
dims=str2double((dim).');
disp(dims);

%      time for start and end of rise and its type
%      time for start and end of fall and its type
rise=menu('type of rise','harmonic','constant acceleration','cyclodial')
disp(rise)
fall=menu('type of fall','harmonic','constant acceleration','cycloidal')
disp(fall)  


if(rise==1)
   t2=linspace(dims(1,2),dims(1,3),(dims(1,3)-dims(1,2))/360*100);
   d2=.5*dims(1,1)*(1-cos((t2-dims(1,2))*pi/(dims(1,3)-dims(1,2))));
endif

if(fall==1)
   t4=linspace(dims(1,4),dims(1,5),(dims(1,5)-dims(1,4))/360*100);
   d4=.5*dims(1,1)*(1+cos((t4-dims(1,4))*pi/(dims(1,5)-dims(1,4))));
endif
t1=d1=linspace(0,dims(1,2),(dims(1,2)/360*100));
d1(1,:)=0;
t3=d3=linspace(dims(1,3),dims(1,4),(dims(1,4)-dims(1,3))/360*100);
d3(1,:)=dims(1,1);
d=[d1,d2,d3,d4];
t=[t1,t2,t3,t4];
figure
plot(t,d)
title('displacement diagram');










%now allowthe user to input the values for cam characteristics like basecircle radii or eccentricity

prompt = {"base circle radii","eccentricity"};
default = {"50","0"};
rowcol = [1,10;1,10;];
char = str2double(inputdlg (prompt, "enter cam characteristics", rowcol, default));
disp(char);
%also ask for type of follower
folr=menu("type of follower","knife edge","roller","flatface");
disp(folr);
if (folr==2)
   prompt = {"roller radii"};
   defalt = {"10"};
   rowco = [1,10;];
   rollr = inputdlg (prompt, "enter roller radii", rowco, defalt);
   disp(rollr);
 endif
 %now we come to the actual calculation and plotting
 
 

 figure
 theta=deg2rad(t);
 r=(char(1,1)+d);
   polar (theta, r, "--b");
   max(r)
 set (gca, "rtick", 0:(max(r)/8):(max(r)*1.2), "ttick", 0:20:340);
 title ("cam profile appearance");
 #x=r.*cos(deg2rad(theta));
 #y=r.*sin(deg2rad(theta));
 #plot(x,y);
 #title('cam profile');
