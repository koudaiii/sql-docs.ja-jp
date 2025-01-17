---
title: 2 つのデータベースのデータを比較および同期する
description: 2 つのデータベースのデータを比較および同期する方法について説明します。 比較の設定、差異の表示、およびターゲットの更新を行う方法を確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.connection.datasources.f1
- sql.data.tools.datacompare.watermark.f1
- sql.data.tools.datacompare.connection.objectselection.f1
ms.assetid: 2148e517-ed42-41c6-b753-1ac625f594c8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 03/22/2021
ms.openlocfilehash: d869aaf652cf3c5d9baa389ab26303ba46049b71
ms.sourcegitcommit: c09ef164007879a904a376eb508004985ba06cf0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104890719"
---
# <a name="how-to-compare-and-synchronize-the-data-of-two-databases"></a>方法:2 つのデータベースのデータを比較および同期する

2 つのデータベースに含まれるデータを比較できます。 比較するデータベースは、*ソース* と *ターゲット* と呼ばれます。  
  
> [!NOTE]  
> *データベース プロジェクト* および .dacpac パッケージまたは .bacpac パッケージは、データ比較のソースまたはターゲットに指定できません。  
  
データを比較すると、*データ操作言語* (DML) スクリプトが生成されます。このスクリプトを使用すると、ターゲット データベースの一部またはすべてのデータを更新して、内容が異なるデータベースを同期することができます。 データの比較が終了すると、Visual Studio の [データ比較] ウィンドウにその結果が表示されます。  
  
比較が完了したら、次のように他の手順を実行できます。  
  
-   2 つのデータベース間の差異を確認できます。 詳しくは、「[データの差異の表示](#ViewDifferences)」をご覧ください。  
  
-   ターゲットの一部またはすべてをソースに一致するよう更新できます。 詳しくは、「[データベース データの同期](#Synchronize)」をご覧ください。  
  
詳しくは、「[1 つ以上のテーブルのデータを参照データベースのデータと比較して同期する](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)」をご覧ください。  
  
> [!NOTE]  
> 2 つのデータベース、または同一データベースの 2 つのバージョンの *スキーマ* も比較できます。 詳細については、「[スキーマ比較を使用して各種のデータベース定義を比較する方法](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)」を参照してください。  
  
## <a name="comparing-database-data"></a><a name="CompareDatabaseData"></a>データベース データの比較  
  
#### <a name="to-compare-data-by-using-the-new-data-comparison-wizard"></a>新しいデータの比較ウィザードを使用してデータを比較するには  
  
1.  **[SQL]** メニューの **[データ比較]** をポイントし、 **[新しいデータの比較]** をクリックします。  
  
    新しいデータの比較ウィザードが表示されます。 また、[データ比較] ウィンドウが開き、DataCompare1 などの名前が Visual Studio によって自動的に割り当てられます。  
  
2.  ソース データベースとターゲット データベースを識別します。  
  
    **[ソース データベース]** ボックスの一覧または **[ターゲット データベース]** ボックスの一覧が空の場合は、 **[新しい接続]** をクリックします。 **[接続のプロパティ]** ダイアログ ボックスで、データベースが存在するサーバー、およびデータベースへの接続時に使用する認証の種類を指定します。 その後、 **[OK]** をクリックして **[接続のプロパティ]** ダイアログ ボックスを閉じ、データの比較ウィザードに戻ります。  
  
    データの比較ウィザードの最初のページで、各データベースの情報が正しいことを確認し、結果に含めるレコードを指定して、**[次へ]** をクリックします。 データの比較ウィザードの 2 ページ目が表示され、データベース内のテーブルとビューが階層形式で表示されます。  
  
3.  比較するテーブルおよびビューのチェック ボックスをオンにします。 必要に応じて、データベース オブジェクトのノードを展開し、そのオブジェクト内で比較する列のチェック ボックスをオンにします。  
  
    > [!NOTE]  
    > テーブルとビューが一覧に表示されるようにするには、2 つの条件を満たす必要があります。 まず、ソース データベースとターゲット データベース間でオブジェクトのスキーマが一致する必要があります。 次に、主キー、一意なキー、一意なインデックス、または一意な制約を持つテーブルとビューのみが一覧に表示されます。 両方の条件を満たすテーブルまたはビューが存在しない場合、一覧は空になります。  
  
4.  複数のキーが存在する場合は、**[比較キー]** 列を使用し、データ比較の基になるキーを指定することができます。 たとえば、主キー列と (一意に識別できる) 他のキー列のどちらを比較の基準にするかを指定できます。  
  
5.  **[完了]** をクリックします。  
  
    比較が開始されます。  
  
    > [!NOTE]  
    > 実行中のデータの比較操作を停止するには、**[SQL]** メニューの **[データ比較]** をクリックし、**[データ比較の停止]** をクリックします。  
  
    比較が完了したら、2 つのデータベース間のデータの差異を表示できます。 ターゲット データベースのデータの一部またはすべては、ソース データベースのデータと一致するよう更新することもできます。  
  
#### <a name="to-compare-data-by-using-the-visual-studio-automation-model"></a>Visual Studio オートメーション モデルを使用してデータを比較するには  
  
1.  **[表示]** メニューを開き、 **[その他のウィンドウ]** をポイントし、 **[コマンド ウィンドウ]** をクリックします。  
  
2.  コマンド ウィンドウで、次のコマンドを入力します。  
  
    ```  
    Tools.NewDataComparison /SrcServerName sServerName /SrcDatabaseName sDatabaseName /SrcUserName sUserName /SrcPassword sPassword /SrcDisplayName sDisplayName /TargetServerName tServerName /TargetDatabaseName tDatabaseName /TargeUserName tUserName /TargetPassword tPassword /TargetDisplayName tDisplayName  
    ```  
  
    プレースホルダー (*sServerName*、*sDatabaseName*、*sUserName*、*sPassword*、*sDisplayName*、*tServerName*、*tDatabaseName*、*tUserName*、*tPassword*、*tDisplayName*) をソース データベースとターゲット データベースの値に置き換えます。  
  
    ソースおよびターゲットを指定しない場合は、 **[新しいデータの比較]** ダイアログ ボックスが表示されます。 Tools.NewDataComparison コマンドのパラメーターの詳細については、[Visual Studio Team System のデータベース機能のオートメーション コマンド リファレンス](/previous-versions/visualstudio/visual-studio-2010/dd470565(v=vs.100))に関するページをご覧ください。  
  
    指定したソース データベースとターゲット データベースのデータが比較されます。 結果が [データ比較] セッションに表示されます。 結果の表示方法またはデータの同期方法について詳しくは、「[データの差異の表示](#ViewDifferences)」および「[データベース データの同期](#Synchronize)」をご覧ください。  
  
## <a name="viewing-data-differences"></a><a name="ViewDifferences"></a>データの差異の表示  
2 つのデータベースのデータを比較すると、[データ比較] ボックスには、比較した各 *データベース オブジェクト* とその状態が一覧表示されます。 各オブジェクト内のレコードの結果を状態別にグループ化して表示することもできます。 状態の指定について詳しくは、「[1 つ以上のテーブルのデータを参照データベースのデータと比較して同期する](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)」をご覧ください。  
  
差異を表示した後、異なる、欠落している、または新しいオブジェクトまたはレコードの一部またはすべてについて、ソースと一致するようにターゲットを更新できます。 詳しくは、「[データベース データの同期](#Synchronize)」をご覧ください。  
  
#### <a name="to-view-data-differences"></a>データの差異を表示するには  
  
1.  ソース データベースとターゲット データベースのデータを比較します。 詳しくは、「[データベース データの比較](#CompareDatabaseData)」をご覧ください。  
  
2.  (省略可能) 次のいずれかまたは両方の操作を行います。  
  
    -   既定では、状態に関係なく、すべてのオブジェクトの結果が表示されます。 特定の状態のオブジェクトのみを表示するには、 **[フィルター]** ボックスの一覧でオプションをクリックします。  
  
    -   特定のオブジェクト内のレコードの結果を表示するには、メインの結果ペインでオブジェクトをクリックし、レコード ビュー ペインでタブをクリックします。 各タブには、そのオブジェクト内で特定の状態 (不一致、ソースのみに存在、ターゲットのみに存在、または一致) にあるすべてのレコードが表示されます。 データは、レコードおよび列ごとに表示されます。  
  
## <a name="synchronizing-database-data"></a><a name="Synchronize"></a>データベース データの同期  
2 つのデータベースのデータを比較した後、ソースと一致するようにターゲットの全体または一部を更新して、2 つのデータベースを同期できます。 テーブルとビューという 2 種類のデータベース オブジェクトのデータを比較できます。  
  
#### <a name="to-update-target-data-by-using-the-write-updates-command"></a>[更新の書き込み] コマンドを使用してターゲット データを更新するには  
  
1.  ソース データベースとターゲット データベースのデータを比較します。 詳しくは、「[データベース データの比較](#CompareDatabaseData)」をご覧ください。  
  
    比較が終了すると、比較したオブジェクトの結果が [データ比較] ウィンドウに表示されます。 4 つの列 ([異なるレコード]、[ソース内のみ]、[ターゲット内のみ]、[一致するレコード]) には、一致しないオブジェクトに関する情報が表示されます。 これらの列には、このような各オブジェクトについて、異なると検出されたレコードの件数、および更新操作によって変更されるレコードの件数が表示されます。 この 2 つの数値は最初一致しますが、手順 4. で、更新するオブジェクトを変更できます。  
  
    詳しくは、「[1 つ以上のテーブルのデータを参照データベースのデータと比較して同期する](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)」をご覧ください。  
  
2.  [データ比較] ウィンドウのテーブルで、任意の行をクリックします。  
  
    詳細ペインに、クリックしたデータベース オブジェクトのレコードに関する結果が表示されます。 レコードは状態別にタブでグループ化されており、このタブを使用して、ソースからターゲットに反映させるデータを指定できます。  
  
3.  詳細ペインで、ゼロ (0) 以外の数字が名前に含まれるタブをクリックします。  
  
    **[ターゲット内のみ]** テーブルの **[更新]** 列のチェック ボックスを使用して、更新する行を選択できます。 既定では、各チェック ボックスがオンになっています。  
  
4.  ターゲットのレコードのうち、ソースのデータで更新しないレコードのチェック ボックスをオフにします。  
  
    チェック ボックスをオフにすると、更新するレコードの数が減るため、この操作を反映するよう表示が変更されます。 この数は、詳細ペインのステータス行、および手順 1. で説明したようにメインの結果ペインの対応する列に表示されます。  
  
5.  (省略可能) **[スクリプトの生成]** をクリックします。  
  
    Transact\-SQL エディター ウィンドウが開き、ターゲットの更新に使用する *データ操作言語* (DML) スクリプトが表示されます。  
  
6.  異なるレコード、欠落しているレコード、または新しいレコードを同期するために、 **[ターゲットの更新]** をクリックします。  
  
    > [!NOTE]  
    > ターゲット データベースの更新中に **[ターゲットへの書き込みの停止]** をクリックすると、操作を取り消すことができます。  
  
    ターゲットで選択されたレコードのデータが、ソース内の対応するレコードのデータで更新されます。  
  
    > [!NOTE]  
    > インデックス付きビューを更新するときに、同一テーブルに重複するキーが挿入される場合は **[ターゲットの更新]** 操作が失敗することがあります。  
  
#### <a name="to-update-target-data-by-using-a-transact-sql-script"></a>Transact\-SQL スクリプトを使用してターゲット データを更新するには  
  
1.  ソース データベースとターゲット データベースのデータを比較します。 詳しくは、「[データベース データの比較](#CompareDatabaseData)」をご覧ください。  
  
    比較が終了すると、比較したオブジェクトが [データ比較] ウィンドウに表示されます。 詳しくは、「[1 つ以上のテーブルのデータを参照データベースのデータと比較して同期する](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)」をご覧ください。  
  
2.  (省略可能) 前の手順で説明したように、詳細ペインで、更新しないターゲットのレコードのチェック ボックスをオフにします。  
  
3.  **[スクリプトの生成]** をクリックします。  
  
    ターゲットのデータをソースのデータに一致させるために必要な変更を反映する Transact\-SQL スクリプトが新しいウィンドウに表示されます。 新しいウィンドウには、**DataUpdate_Database_1.sql** のような名前が付いています。  
  
    このスクリプトは、詳細ペインで行った変更を反映しています。 たとえば、[ターゲット内のみ] ページで [dbo].[Shippers] テーブルの特定の行のチェック ボックスをオフにしたとします。 その場合、スクリプトではその行が更新されません。  
  
4.  (省略可能) **[DataUpdate_Database_1.sql]** ウィンドウでこのスクリプトを編集します。  
  
5.  (省略可能、ただし推奨) ターゲット データベースをバックアップします。  
  
6.  **[実行]** をクリックして、ターゲット データベースを更新します。  
  
    更新するターゲット データベースへの接続を指定します。  
  
    > [!IMPORTANT]  
    > 既定では、更新はトランザクションのスコープ内で実行されます。 エラーが発生した場合は、更新全体をロールバックできます。 この動作は変更できます。  
  
    ターゲットで選択されたレコードのデータが、ソース内の対応するレコードのデータで更新されます。  
  
## <a name="see-also"></a>参照  
[1 つ以上のテーブルのデータを参照データベースのデータと比較して同期する](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)  
