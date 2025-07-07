 1. classdef app1 < matlab.apps.AppBase
 2.  
 3.     % Properties that correspond to app components
 4.     properties (Access = public)
 5.         UIFigure      matlab.ui.Figure
 6.         Label         matlab.ui.control.Label
 7.         UploadButton  matlab.ui.control.Button
 8.         UIAxes2       matlab.ui.control.UIAxes
 9.         UIAxes        matlab.ui.control.UIAxes
10.     end 
11.   
12.      
13.     methods (Access = private) 
14.          
15.         function BW = C2B(app, X) 
16.             X = imadjust(X); 
17.             BW = imbinarize(X); 
18.         end 
19.     end 
20.      
21.   
22.     % Callbacks that handle component events 
23.     methods (Access = private) 
24.   
25.         % Button pushed function: UploadButton 
26.         function UploadButtonPushed(app, event) 
27.             [filename, pathname] = uigetfile({'*.png;*.jpg;*.jpeg;*.bmp', 'Image Files (*.png, *.jpg, *.jpeg, *.bmp)'}, 'Select an Image File'); 
28.   
29.             % Check if the user clicked Cancel 
30.             if isequal(filename, 0) || isequal(pathname, 0) 
31.                 return; 
32.             end 
33.   
34.             % Read the selected image file 
35.             fullFilePath = fullfile(pathname, filename); 
36.             img = imread(fullFilePath); 
37.   
38.             % Get the size of the original image 
39.             [height, width, ~] = size(img); 
40.   
41.             if height < 1000 || width < 1000 
42.                 % Display an error message 
43.                 errordlg('Image dimensions must be at least 1000x1000 pixels.', 'Image Size Error'); 
44.                 return;  % Abort further processing 
45.             end 
46.   
47.             % Change backgroound color of Axes component 
48.             app.UIAxes.Color = [0.7, 0.7, 0.7]; 
49.             app.UIAxes2.Color = [0.7, 0.7, 0.7]; 
50.   
51.             % Display the image on the Axes component 
52.             imshow(img, 'Parent', app.UIAxes); 
53.             sqr=[400,400,1000,1000] 
54.   
55.             % Draw the square on the original image 
56.             rectangle('Position', sqr, 'EdgeColor', 'r', 'LineWidth', 2, 'Parent', app.UIAxes); 
57.   
58.             A = imadjust(rgb2gray(img)); % Change the image to grayscale 
59.             I1 = imcrop(A,sqr); % Crop the image  
60.             BW1 = app.C2B(I1);   
61.             IMG1 = (sum(BW1,'all')/(1001^2)) * 100 
62.   
63.             IMG1 = sprintf('%.2f', IMG1); % Round IMG1 to two decimal places 
64.   
65.             % Concatenate the string and number 
66.             combinedText = ['Ductile Removal: ', IMG1, '%']; 
67.   
68.             app.Label.Text = combinedText; 
69.             imshow(BW1, 'Parent', app.UIAxes2); 
70.         end 
71.     end 
72.   
73.     % Component initialization 
74.     methods (Access = private) 
75.   
76.         % Create UIFigure and components 
77.         function createComponents(app) 
78.   
79.             % Create UIFigure and hide until all components are created 
80.             app.UIFigure = uifigure('Visible', 'off'); 
81.             app.UIFigure.Position = [100 100 861 649]; 
82.             app.UIFigure.Name = 'MATLAB App'; 
83.   
84.             % Create UIAxes 
85.             app.UIAxes = uiaxes(app.UIFigure); 
86.             zlabel(app.UIAxes, 'Z') 
87.             app.UIAxes.TickLabelInterpreter = 'none'; 
88.             app.UIAxes.Position = [3 165 424 381]; 
89.   
90.             % Create UIAxes2 
91.             app.UIAxes2 = uiaxes(app.UIFigure); 
92.             zlabel(app.UIAxes2, 'Z') 
93.             app.UIAxes2.Position = [427 165 424 381]; 
94.   
95.             % Create UploadButton 
96.             app.UploadButton = uibutton(app.UIFigure, 'push'); 
97.             app.UploadButton.ButtonPushedFcn = createCallbackFcn(app, @UploadButtonPushed, true); 
98.             app.UploadButton.Position = [370 110 124 38]; 
99.             app.UploadButton.Text = 'Upload'; 
100.  
101.             % Create Label
102.             app.Label = uilabel(app.UIFigure);
103.             app.Label.HorizontalAlignment = 'center';
104.             app.Label.FontSize = 24;
105.             app.Label.FontWeight = 'bold';
106.             app.Label.Position = [35 28 794 63];
107.             app.Label.Text = '';
108.  
109.             % Show the figure after all components are created
110.             app.UIFigure.Visible = 'on';
111.         end
112.     end
113.  
114.     % App creation and deletion
115.     methods (Access = public)
116.  
117.         % Construct app
118.         function app = app1
119.  
120.             % Create UIFigure and components
121.             createComponents(app)
122.  
123.             % Register the app with App Designer
124.             registerApp(app, app.UIFigure)
125.  
126.             if nargout == 0
127.                 clear app
128.             end
129.         end
130.  
131.         % Code that executes before app deletion
132.         function delete(app)
133.  
134.             % Delete UIFigure when app is deleted
135.             delete(app.UIFigure)
136.         end
137.     end
138. end 
 
