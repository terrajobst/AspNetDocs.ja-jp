> <span data-ttu-id="852f6-101">アプリが Id データストアとして SQLite を使用している場合、一部のコマンドはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="852f6-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="852f6-102">データベースエンジンの制限により、`Alter` のコマンドは次の例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="852f6-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="852f6-103">"NotSupportedException: SQLite は、この移行操作をサポートしていません。"</span><span class="sxs-lookup"><span data-stu-id="852f6-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="852f6-104">回避策として、データベースで Code First の移行を実行してテーブルを変更します。</span><span class="sxs-lookup"><span data-stu-id="852f6-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
