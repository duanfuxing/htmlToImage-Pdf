# htmlToImage-Pdf
基于wkhtmltoimage 使用的Qt WebKit渲染引擎将HTML呈现为PDF和图像格式


安装wkhtmltopdf 

	官网地址：https://wkhtmltopdf.org
	简书文档地址：http://www.jianshu.com/p/4d65857ffe5e
	1.夸平台Liunx,Windows,Mac
	2.有64位，32位安装文件pdf和image
	3.下载安装 ：https://wkhtmltopdf.org/downloads.html
	4.设置环境变量(全局)


Laravel使用方式

	文档：https://github.com/barryvdh/laravel-snappy

	1.下载laravel-snappy组件 
		composer require barryvdh/laravel-snappy
		
	2.在 config/app.php添加以下内容

		providers数组中添加 
			Barryvdh\Snappy\ServiceProvider::class,
			
		aliases数组中添加
			'PDF' => Barryvdh\Snappy\Facades\SnappyPdf::class,
			'SnappyImage' => Barryvdh\Snappy\Facades\SnappyImage::class,

	3.生成对应文件映射

		php artisan vendor:publish --provider="Barryvdh\Snappy\ServiceProvider"
			
			
	4.配置snappy文件
	
		修改binary数值（双引号中修改成wkhtmltopdf安装的绝对路径）
			PDF
				windows：'binary'  => '"C:\Program Files\wkhtmltopdf\bin\wkhtmltopdf.exe"',  
				linux  ：'binary'  => '/usr/local/bin/wkhtmltopdf-amd64',   
				composer安装：'binary' => base_path('vendor/h4cc/wkhtmltopdf-amd64/bin/wkhtmltopdf-amd64'),
			IMAGE
				windows：'binary'  => '"C:\Program Files\wkhtmltopdf\bin\wkhtmltoimage.exe"',  
				linux  ：'binary'  => '/usr/local/bin/wkhtmltoimage-amd64',   
				composer安装：'binary' => base_path('vendor/h4cc/wkhtmltopdf-amd64/bin/wkhtmltoimage-amd64'),

	5.使用
	
		1).直接显示在页面中

			$pdf = App::make('snappy.pdf.wrapper'); //转PDF snappy.pdf.wrapper   转image snappy.image.wrapper
			$content = 'HTML代码';  页面中有中文一定要指定字符集{<meta http-equiv="content-type" content="text/html;charset=utf-8">}
			$pdf->loadHTML($content);
			return $pdf->inline();
			
		2).保存成文件

			$snappy = App::make('snappy.pdf');//转PDF snappy.pdf   转Image snappy.image
			$html = 'HTML代码';
			$snappy->generateFromHtml($html, '/tmp/123.pdf');
			$snappy->generate('http://www.baidu.com', '/tmp/213.pdf');
			
		3).下载
			
			return PDF::loadView('pdf.invoice', $data)->download('invoice.pdf');
					

************************************************************************************************

	php组件
		文档地址：https://packagist.org/packages/mikehaertl/phpwkhtmltopdf
	




