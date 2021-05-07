# Aplikasi_Perbaikan_Citra
Aplikasi GUI untuk memperbaiki noise pada gambar dengan metode median filter
~~~
Nama  : Arif Samsudin
NIM   : 311910255
Kelas : TI 19 C1
~~~
# 1. Persiapan Membuat Aplikasi GUI
ketik guide pada command windows lalu tekan enter
![1  guide](https://user-images.githubusercontent.com/81839328/117487377-36d74e80-af95-11eb-9bc2-b225c807e302.JPG)

# 2. Creat New GUI
Pilih creat new GUI, tentukan lokasi penyimpanan lalu tekan OK
![2  new gui](https://user-images.githubusercontent.com/81839328/117487412-422a7a00-af95-11eb-9e5a-36fc2c90964b.JPG)

# 3. Buat Tampilan GUI sesuai kebutuhan
![3  Buat tampilan gui](https://user-images.githubusercontent.com/81839328/117487691-9b92a900-af95-11eb-971e-953d43667f74.JPG)

# 4. Buat Source Code
Untuk memanggil tombol fungsi pada source klik kanan pada tombol fungsi >> view callback >> callback
![4  callback](https://user-images.githubusercontent.com/81839328/117487831-cd0b7480-af95-11eb-8835-2db1a0bdefc4.png)

Membuat Source Code
~~~
% --- Executes just before UTS is made visible.
function UTS_OpeningFcn(hObject, eventdata, handles, varargin)
% This function has no output args, see OutputFcn.
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% varargin   command line arguments to UTS (see VARARGIN)

% Choose default command line output for UTS
handles.output = hObject;

% Update handles structure
guidata(hObject, handles);

% UIWAIT makes UTS wait for user response (see UIRESUME)
% uiwait(handles.figure1);


% --- Outputs from this function are returned to the command line.
function varargout = UTS_OutputFcn(hObject, eventdata, handles) 
% varargout  cell array for returning output args (see VARARGOUT);
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Get default command line output from handles structure
varargout{1} = handles.output;


% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
[filename, pathname] = uigetfile({'*.jpg','*.png'});

citra1 = imread ([pathname, filename]);
%menampilkan di axes
axes(handles.axes1);
imshow(citra1);
[tinggiA, lebarA] = size(citra1);

%proses filter median untuk citra mobil
for baris=2 : tinggiA-1
    for kolom=2 : lebarA-1
        dataA = [citra1(baris-1, kolom-1) citra1(baris-1, kolom) citra1(baris-1, kolom+1)  ...
              citra1(baris, kolom-1) citra1(baris, kolom) citra1(baris, kolom+1)  ...
              citra1(baris+1, kolom-1) citra1(baris+1, kolom) citra1(baris+1, kolom+1)];
        
        % Urutkan
        for i=1 : 8
            for j=i+1 : 9
                if dataA(i) > dataA(j)
                    tmpA = dataA(i);
                    dataA(i) = dataA(j);
                    dataA(j) = tmpA;
                end
            end
        end 
        
        % Ambil nilai median
        citra2(baris, kolom) = dataA(5);
    end
end

%menampilkan di axes2
axes(handles.axes2);
imshow(citra2);
~~~
![5  source](https://user-images.githubusercontent.com/81839328/117487838-cf6dce80-af95-11eb-997e-24b6d36c665a.JPG)


