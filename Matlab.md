`edit <fname>`: create new file as 'fname.m' and open it  
`$ fname`: run 'fname.m' in command line  
`whos`: show the variables in the workspace  
`ans`: most recent result  
`clear`: clear all variables  
`clc`: clear command window  
`%`: comments

`doc <func>`  
`help <func>`

`edit(fullfile(userpath,'startup.m'))`: creates a new startup file if one doesn't exist already; add initialization commands & save into the file; re-open Matlab will automatically go through the configs

`x = dir('...\...\');`: `x.name` are the files inside the directory

---

```matlab
if ...
    ...
elseif ...
else
end
```

```matlab
for i = i1:di:i2
    ...
end
```

---

### Structure

[structure](https://www.mathworks.com/help/matlab/structures.html)

```matlab
X.y = ...     % create a scalar structure with field y
X(N).y = ...  % create a structure array with N elements
```

### Strings

`num2str(N)`  
`fnumber = sprintf(‘%0Nd’,number);`: fnumber has N characters, if number is too short, add 0 to the front

`isspace(x)`: return indices where the character is a whitespace, e.g. `x(~isspace(x))` removes all white  
`strtrim(x)`: remove whitespace in the beginning & the end

`lower(x)`: return lower cases

`strcmp(x, y)`: True if x = y

### Cells

`x = cell(N1, N2);`: initialize  
`x{i, j} = ...;`

---

### functions

`rand(Nrow, Ncol)`

`[..., ...; ..., ...]`: concaternation; ',' - attach new columns; ';' - attach new rows

`fix(x)`, `ceil(x)`, `floor(x)`, `round(x, N)`

solution optimization:
```matlab
y = ...;
f = @(x) func_name(x, y, ...);         % x will be optimized; y is fixed; func_name defined in another file

options = optimset('Display','iter', ...           % display to command window (iter - each iteration)
                   'PlotFcns',@optimplotfval, ...  % plot history
                   'TolX', 1e-N, ...               % dx < TolX
		   'TolFun', 1e-N, 'MaxIter', N);  % df < TolFun; only for fminsearch

[x, fval, exitflag, output] = fminsearch(f, x0, options); % stops when df < TolFun && dx < TolX

[x, fval, exitflag, output] = fzero(f, x0, options);
```

---

### plots

`histogram(y,N,'Normalization','cdf');`: N - no. of bins; 'cdf' - cumulative distribution from 0 to 1

```matlab
clr1 = [...]; clr2 = [...];
dclr = clr2-clr1;
...
cnt = 0;
for loop % nn points in total
    clr = clr1+cnt/(nn-1)*dclr;
    cnt = cnt+1;
    plot(..., 'Color',clr); % line colors varying from clr1 to clr2
end
```

```matlab
mesh(<x>, <y>, z)
[xgrid, ygrid] = meshgrid(linspace(xmin, xmax), linspace(ymin, ymax))
```

```matlab
z2 = griddata(x, y, z, xgrid, ygrid, 'linear') # interpolate z values (given at x, y) to xgrid & ygrid

surf(<x>, <y>, z)
contourf(x, y, z, [-aa, linspace(-a,b,N), bb]); % no white spots
caxis([-a b]);
```

`rectangle('Position', [x, y, width, height], 'Curvature', [f1, f2], 'FaceColor', ...)`: `[x,y]` is left-bottom vertex; `f1=f2=1` gives a circle  

```matlab
h = subplot(a,b,i);
p = get(h,'pos'); % [left, bottom, width, height] in percentage of plot-box size
# change p value
set(h, 'pos', p);
```

```matlab
axes('Position',[left, bottom, width, height],'Visible','off'); % this is to start a new axis outside the current range
text(x,y,'text'); % text outside the range of the figure
```

```matlab
hp3 = get(subplot(3,1,3),'Position');
colorbar('Position',... % one colorbar for all subplots
         [hp3(1)+hp3(3)+0.01  hp3(2)  0.03  hp3(2)+hp3(4)*3]);
```

```matlab
fttl = ['$',fttl,'$']; 	% fttl is the string containing Latex
h = title(fttl,'FontSize',14); 	% title / xlabel / ylabel
set(h,'interpreter','latex')
```


---

### Input & Output

`fprintf('format', x, y, …)`: output to screen  
`disp('...')`: show texts in command window

```matlab
save <fname>
load <fname>
```

```matlab
prompt = 'text on screen';
n = input(prompt); % read input from the screen
```

```matlab
fid = fopen(fname); % read from text or dat file
data = textscan(fid,'%f', 'HeaderLines',a, ... % skip a lines of headline
                'delimiter','\t'); % '\t' separates each data entry
fclose(fid);
data = data{1};
```

```matlab
t = readtable(fname, 'delimiter', '...');
columns = t.Properties.VariableNames;
```

```matlab
fileID = fopen(name,'a'); % 'w'; 'a' to appendix to existing files
fprintf(fileID,'%.8e\n',x); % write x to the file
fclose(fileID);
```

```matlab
handle = figure;
h = figure('Renderer', 'painters', 'Position', [Nx Ny Width Height]) % typical pixel is [0, 0, 1800, 900]
print(handle,'format',filename) % 'format':	'-depsc' (eps color), '-djpeg' (jpeg file)
% or
saveas(gcf,name,'epsc'); % no need to put file extension
```

```matlab
for imov = 1:n;
		mov(imov) = getframe(gcf);
end
movie2avi(mov,'fname.avi','fps',m,'compression','None');
% or
writerObj = VideoWriter(fname,'MPEG-4'); % fname is the name of the video; other format e.g. 'Uncompressed AVI'
writerObj.FrameRate = 2;
open(writerObj);
for i = 1:n;
    h = figure;
    % configure your plot
    frame = getframe(h);
    writeVideo(writerObj,frame);
    pause(1); % this line is only necessary when you want to view the movie as it produces
    close(h);
end
close(writerObj);
```


---

### Database

```matlab
conn = database('database_name', 'username', 'password', …
                'Vendor', 'database_type', …        % 'MySQL', 'PostgreSQL', …
                'Server', 'server_name_or_address');
conn = database('dataSource', ... % first configure 'dataSource' in 'Apps/Database Explorer' and save
                'username', 'password');
...
close(conn)
```

`files = catalogs(conn);`: all existing database

`ts = tables(conn, 'file');`: all tables in the catalog

`cols = columns(conn, 'file');`: all columns in the catalog

`results = runsqlscript(conn, fname);`: `fname` is a sql file

```matlab
data = exec(conn, selectquery); % selectquery is a string
data = fetch(data);
data = data.Data;
```

To setup connection to [MySQL database](https://www.mathworks.com/help/database/ug/mysql-jdbc-windows.html#bt8knx3-3):  
1. Method 1:
	- Download JDBC driver for MySQL
	- Unzip and move the .jar file to matlab folder (`…\MATLAB\R2016b\java\jarext\`)
	- `>> prefdir` in matlab, open the path, close Matlab
	- Create `javaclasspath.txt` file in the preferred path
	- Write the full path of .jar file (with file name), save
	- Restart Matlab
2. Method 2:
	- install mysql connector
	- run `javaaddpath 'C:\Program Files (x86)\MySQL\Connector J 5.1\mysql-connector-java-5.1.49.jar'` in Matlab (can be added to `startup.m` for auto setup)


---

### Deploy Applications

To compile Matlab app:
- Go to APPS and click 'Production Server Compiler'
- Select 'Deployable Archive (.ctf)'
- Use '+' to add all files needed
- Edit archive name
- Save
- Package
- The .ctf file in 'for redistribution' can be pushed to server
