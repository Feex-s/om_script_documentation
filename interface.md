# Интренфейсы Scripts API с пояснениями:

##Интерфейс Cell:
```
interface Cell {
    setValue(value: number | string | null);

    getValue(): number | string | null;

    getNativeValue(): number | string | null;

    getTextValue(): number | string | null;

    getContextValue(): string | null;

    definitions(): number[];

    columns(): LabelsGroup;

    rows(): LabelsGroup;

    dropDown(): Labels;

    getFormatType(): string;
}
```
***

##Интерфейс Cells:
```
interface Cells {
    all(): Cell[];

    first(): Cell;

    setValue(value: number | string | null);

    count(): number;

    chunkInstance(): GridRangeChunk;

    getByIndexes(indexes: number[]): Cells | null;
}
```
***
##Интерфейс Label:
```
interface Label {
    longId(): number;

    name(): string;

    code(): string;

    alias(): string | null;

    label(): string | null;

    parentLongId(): number;
}
```
***
##Интерфейс LabelsGroup:
```
interface LabelsGroup {
    all(): Label[];

    first(): Label;

    cells(): Cells;
}
```
***
##Интерфейс Labels:
```
interface Labels {
    start(): number;

    count(): number;

    all(): LabelsGroup[];

    get(index: number): LabelsGroup | null;

    chunkInstance(): GridRangeChunk;

    findLabelByLongId(longId: number): Label | null;
}
```
***
##Интерфейс GridRangeChunk:
```
interface GridRangeChunk {
    cells(): Cells;

    rows(): Labels;

    columns(): Labels;
}
```
***
##Интерфейс GridRange:
```
interface GridRange {
    rowStart(): number;

    rowCount(): number;

    columnStart(): number;

    columnCount(): number;

    cellCount(): number;

    generator(size?: number): GridRangeChunk[];
}
```
***
##Интерфейс GridDimension:
```
interface GridDimension
{
    getDimensionEntity(): EntityInfo;
}
```
***
##Интерфейс GridDefinitionInfo:
```
interface GridDefinitionInfo
{
    getPageSelectors(): GridPageSelector[];

    getRowDimensions(): GridDimension[];

    getColumnDimensions(): GridDimension[];
}
```
***
##Интерфейс Grid:
```
interface Grid {
    range(rowStart?: number, rowCount?: number, columnStart?: number, columnCount?: number): GridRange;

    rowCount(): number;

    columnCount(): number;

    cellCount(): number;

    getDefinitionInfo(): GridDefinitionInfo;

    exporter(): Exporter;
}
```
***
##Интерфейс ExportResult:
```
interface ExportResult {
    mergeToExternalExcelSheet(toFile: string, toSheet: string, fromSheet?: string): ExportResult

    getHash(): string;
}
```
***
##Интерфейс Exporter:
```
interface Exporter {
    setEncoding(encoding: string): Exporter;

    setExtension(extension: string): Exporter;

    setOmitSummaryRows(omitSummaryRows: boolean): Exporter;

    setOmitEmptyRows(omitEmptyRows: boolean): Exporter;

    setIncludeCodes(includeCodes: boolean): Exporter;

    setMappingForFlexibleImport(mappingForFlexibleImport: boolean): Exporter;

    setMappingForAdvancedImport(mappingForAdvancedImport: boolean): Exporter;

    setFileName(fileName: string): Exporter;

    setDelimiter(delimiter: string): Exporter;

    setEnclosure(enclosure: string): Exporter;

    setEscape(escape: string): Exporter;

    setShowAliasesWithoutNames(showAliasesWithoutNames: boolean): Exporter;

    setUseCodeLikeLabels(useCodeLikeLabels: boolean): Exporter;

    export(): ExportResult;
}
```
***
##Интерфейс Pivot:
```
interface Pivot {
    create(): Grid;

    rowsFilter(data: string[] | string | number | number[]): Pivot;

    columnsFilter(data: string[] | string | number | number[]): Pivot;

    withoutValues(): Pivot;

    addDependentContext(identifier: number): Pivot
}
```
***
##Интерфейс NumericElementsCreator:
```
interface NumericElementsCreator {
    setCount(count: number): NumericElementsCreator;

    setPositionAfter(relativeLongId: number): NumericElementsCreator;

    setPositionBefore(relativeLongId: number): NumericElementsCreator;

    setPositionStart(): NumericElementsCreator;

    setPositionEnd(): NumericElementsCreator;

    setPositionChildOf(parentLongId: number): NumericElementsCreator;

    create(): number[];
}
```
***
##Интерфейс ElementsCreator:
```
interface ElementsCreator {
    numeric(): NumericElementsCreator;
}
```
***
##Интерфейс ElementsDeleter:
```
interface ElementsDeleter {
    appendIdentifier(identifier: number): ElementsDeleter;

    delete(): ElementsDeleter;
}
```
***
##Интерфейс ElementsReorder:
```
interface ElementsReorder {
    append(longId: number, relativeLongId: number, position: string): ElementsReorder;

    reorder(): ElementsReorder;

    count(): number;

    reverse(): ElementsReorder;
}
```
***
##Интерфейс Tab:
```
interface Tab {
    pivot(viewName?: string): Pivot;

    open(name: string): Tab;

    elementsCreator(): ElementsCreator;

    elementsDeleter(): ElementsDeleter;

    elementsReorder(): ElementsReorder;

    importer(): Importer;
}
```
***
##Интерфейс Environment:
```
interface Environment {
    load(name: string): Environment;

    get(key: string, def?: any): any;

    set(name: string, value: number | string | null): Environment;
}
```
***
##Интерфейс CubeCell:
```
interface CubeCell{
    definitions(): number[];

    getDimensionIds(): number[];

    getDimensionItems(): EntityInfo[];

    getValue(): number | string | null | boolean;
}
```
***
##Интерфейс CubeCellSelector:
```
interface CubeCellSelector{
    getCubeInfo(): CubeInfo;

    getCubeIdentifier(): number;

    getCubeDimensions(): EntityInfo[];

    // @ts-ignore
    generator(): IterableIterator<CubeCell>;
}
```
***
##Интерфейс CubeCellSelectorBuilder:
```
interface CubeCellSelectorBuilder {
    setFormula(formula: string): this;

    load(): CubeCellSelector;
}
```
***
##Интерфейс CubeCellUpdater:
```
interface CubeCellUpdater{
    getCount(): number;
}
```
***
##Интерфейс CubeCellUpdaterBuilder:
```
interface CubeCellUpdaterBuilder {
    setConditionFormula(formula: string): this;

    setFormula(formula: string): this;

    load(): CubeCellUpdater;
}
```
***
##Интерфейс CubeFormatInfo:
```
interface CubeFormatInfo {
    getFormatTypeEntity(): EntityInfo;

    getDimensionEntity(): EntityInfo | null;
}
```
***
##Интерфейс CubeInfo:
```
interface CubeInfo extends EntityInfo {
    getFormula(): string | null;

    getFormatInfo(): CubeFormatInfo;

    getDimensions(): EntityInfo[];
}
```
***
##Интерфейс MulticubeTab:
```
interface MulticubeTab extends Tab {
    cleanCellsData(cubesIdentifiers?: number[]): MulticubeTab;

    cubeCellSelector(identifier: string | number): CubeCellSelectorBuilder;

    cubeCellUpdater(identifier: string | number): CubeCellUpdaterBuilder;

    getCubeInfo(identifier: string | number): CubeInfo;
}
```
***
##Интерфейс MulticubesTab:
```
interface MulticubesTab extends Tab {
    open(name: string): MulticubeTab;
}
```
***
##Интерфейс Multicubes:
```
interface Multicubes {
    multicubesTab(): MulticubesTab;
}
```
***
##Интерфейс Times:
```
interface Times {
    optionsTab(): Tab

    resetForm(): any;

    applyForm(): any;
}
```
***
##Интерфейс VersionsTab:
```
interface VersionsTab {
    copyVersion(from: string, to: string): any;
}
```
***
##Интерфейс Versions:
```
interface Versions {
    versionsTab(): VersionsTab
}
```
***
##Интерфейс CSVParams:
```
interface CSVParams {
    setDelimiter(delimiter: string): CSVParams;

    getDelimiter(): string;

    setEnclosure(enclosure: string): CSVParams;

    getEnclosure(): string;

    setEscape(escape: string): CSVParams;

    getEscape(): string;

    setLineDelimiter(escape: string): CSVParams;

    getLineDelimiter(): string;
}
```
***
##Интерфейс CubeCellSelectorBuilder:
```
interface CubeCellSelectorBuilder {
    setFormula(formula: string): this;

    load(): CubeCellSelector;
}
```
***
##Интерфейс Importer:
```
interface Importer {
    csv(): CSVParams;

    setFilePath(path: string): Importer;

    getFilePath(): string;

    getReportFilePath(): string

    import(): Importer;
}
```
***
##Интерфейс ListImporter:
```
interface ListImporter extends Importer {
    setFilePath(path: string): ListImporter;

    setObligatoryListCodes(obligatoryListCodes: boolean): ListImporter

    getObligatoryListCodes(): boolean;

    setImportToChildListOnly(importToChildListOnly: boolean): ListImporter;

    getImportToChildListOnly(): boolean;

    setUpdatedPropertiesOnParentLevels(updatedPropertiesOnParentLevels: boolean): ListImporter;

    getUpdatedPropertiesOnParentLevels(): boolean;
}
```
***
##Интерфейс ListTab:
```
interface ListTab extends Tab {
    listSubsetTab(): ListSubsetsTab;

    importer(): ListImporter;
}
```
***
##Интерфейс ListSubsetsTab:
```
interface ListSubsetsTab extends Tab {
    listTab(): ListTab;
}
```
***
##Интерфейс ListsTab:
```
interface ListsTab extends Tab {
    open(name: string): ListTab;
}
```
***
##Интерфейс Lists:
```
interface Lists {
    listsTab(): ListsTab
}
```
***
##Интерфейс CellBuffer:
```
interface CellBuffer {
    set(cell: Cell | CubeCell, value: number | string | null): CellBuffer;

    apply(): CellBuffer;

    count(): number;

    canLoadCellsValues(value: boolean): CellBuffer;
}
```
***
##Интерфейс RequestManager:
```
interface RequestManager {
    log(message: string, print?: boolean): RequestManager;

    logStatusMessage(message: string, print?: boolean): RequestManager;

    setStatusMessage(message: string): RequestManager;
}
```
***
##Интерфейс UserInfo:
```
interface UserInfo {
    getEntity(): EntityInfo;

    getEmail(): string;

    getFirstName(): string;

    getLastName(): string;

    getRole(): EntityInfo;
}
```
***
##Интерфейс ModelInfo:
```
interface ModelInfo {
    id(): number;

    name(): string;

    lastSyncDate(): number;

    autoCalcStatus(): boolean;

    setModelCalculationMode(status: boolean): boolean;

    repair(): boolean;

    recalculate(): boolean;
}
```
***
##Интерфейс ResultInfo:
```
interface ResultInfo {
    addFileHash(hash: string): ResultInfo
}

```
***
##Интерфейс EntityInfo:
```
interface EntityInfo extends Label {
    // уточнить у Николая, должно ли в данном месте быть просто наследование
}
```
***
##Интерфейс EntitiesInfo:
```
interface EntitiesInfo {
    get(longId: number): EntityInfo | null;

    getCollection(longId: number[]): EntityInfo[];
}
```
***
##Интерфейс CopyData:
```
interface CopyData {
    setSourceLongId(longId: number): CopyData;

    setDestLongId(longId: number): CopyData;

    enableCopyAllCubes(): CopyData;

    enableCustomProperties(): CopyData;

    setMulticubeLongIds(longIds: number[]): CopyData;

    setMulticubeByNames(names: string[]): CopyData;

    copy(): CopyData;
}
```
***
##Интерфейс Common:
```
interface Common {
    createCellBuffer(): CellBuffer;

    requestInfo(): RequestManager;

    modelInfo(): ModelInfo;

    userInfo(): UserInfo;

    resultInfo(): ResultInfo;

    entitiesInfo(): EntitiesInfo;

    copyData(): CopyData;
}
```
***
##Интерфейс FileMeta:
```
interface FileMeta {
    type: string;
    path: string;
    visibility: string;
    size: number;
    dirname: string;
    basename: string;
    extension: string;
    filename: string;
}
```
***
##Интерфейс Filesystem:
```
interface Filesystem {
    has(path: string): boolean;

    read(path: string): string;

    readAndDelete(path: string): string;

    write(path: string, contents: string): boolean;

    delete(path: string): boolean;

    rename(from: string, to: string): boolean;

    copy(from: string, to: string): boolean;

    getTimestamp(path: string): string;

    getSize(path: string): number;

    createDir(path: string): boolean;

    deleteDir(path: string): boolean;

    listContents(path: string, recursive: boolean): Array<FileMeta>;

    getMetadata(path: string): object;

    upload(from: string, to: string): boolean;

    download(from: string, to: string): boolean;

    makeGlobalFile(name: string, extension: string, path: string, copy?: boolean): string;

    getPathObj(path: string): PathObj;
}
```
***
##Интерфейс PathObj:
```
interface PathObj {
    getSystem(): Filesystem;

    getPath(): string;
}
```
***
##Интерфейс BaseAdapter:
```
interface BaseAdapter {
    load(): Filesystem;
}
```
***
##Интерфейс FTPAdapter:
```
interface FTPAdapter extends BaseAdapter {
    setHost(host: string): FTPAdapter;

    getHost(): string;

    setPort(port: number): FTPAdapter;

    getPort(): number;

    setUsername(username: string): FTPAdapter;

    getUsername(): string;

    setPassword(password: string): FTPAdapter;

    getPassword(): string;

    setRoot(root: string): FTPAdapter;

    getRoot(): string;

    setPassive(passive: boolean): FTPAdapter;

    getPassive(): boolean;

    setSsl(ssl: boolean): FTPAdapter;

    getSsl(): boolean;

    setTimeout(timeout: number): FTPAdapter;

    getTimeout(): number;

    setUseListOptions(useListOptions: boolean): FTPAdapter;

    getUseListOptions(): boolean;
}
```
***
##Интерфейс CsvReader:
```
interface CsvReader {
    params(): CSVParams;

    /**
     * UTF-8, WINDOWS-1251
     * @param charset
     */
    changeFileCharset(charset: string): CsvReader;

    generator(): [][];
}
```
***
##Интерфейс CsvWriter:
```
interface CsvWriter {
    params(): CSVParams;

    writeRow(row: string[]): CsvWriter;

    writeRows(rows: string[][]): CsvWriter;

    /**
     *
     * @param name
     * @param charset UTF-8, WINDOWS-1251
     */
    save(name: string, charset?: string): string;
}
```
***
##Интерфейс BaseConverter:
```
interface BaseConverter {
    setSource(path: string): this;

    convert(): string;
}
```
***
##Интерфейс ExcelToCsvConverter:
```
interface ExcelToCsvConverter extends BaseConverter {
    setSheetIdentifier(identifier: string | number): this;
}
```
***
##Интерфейс ConverterManager:
```
interface ConverterManager {
    excelToCsv(): ExcelToCsvConverter
}
```
***
##Интерфейс FilesDataManager:
```
interface FilesDataManager {
    csvWriter(): CsvWriter;

    csvReader(path: PathObj): CsvReader;

    converterManager(): ConverterManager;
}
```
***
##Интерфейс Filesystems:
```
interface Filesystems {
    ftp(): FTPAdapter;

    local(): Filesystem;

    sharedFolder(id: string): Filesystem;

    filesDataManager(): FilesDataManager;
}
```
***
##Интерфейс OptimizationRequestTab:
```
interface OptimizationRequestTab extends Tab {
    run(name: string): { success: boolean, error: undefined | string };
}
```
***
##Интерфейс Optimization:
```
interface Optimization {
    optimizationRequestsTab(): OptimizationRequestTab
}
```
***
##Интерфейс SqlQueryResult:
```
interface SqlQueryResult {
    count(): number;

    generator(likeArray?: boolean): object[];

    all(): object[];

    first(): object;

    column(columnName: string): any[];

    cell(columnName: string, rowIndex?: number): number | string | boolean | null;

    updated(): number;

    lastId(): number;
}
```
***
##Интерфейс SqlQueryBuilder:
```
interface SqlQueryBuilder {
    execute(sql: string, bindings?: object): SqlQueryResult;
}
```
***
##Интерфейс SqlConnection:
```
interface SqlConnection {
    qb(): SqlQueryBuilder;
}
```
***
##Интерфейс SqlConnectorBuilder:
```
interface SqlConnectorBuilder {
    setHost(value: string): this;

    setPort(value: number): this;

    setUsername(value: string): this;

    setPassword(value: string): this;

    setDatabase(value: string): this;

    /**
     * https://docs.microsoft.com/ru-ru/sql/tools/bcp-utility
     */
    loadBulkCopyBuilder(): SqlBulkCopyBuilder;

    load(): SqlConnection;
}
```
***
##Интерфейс SqlBulkCopyResult:
```
interface SqlBulkCopyResult {
    hasErrors(): boolean;

    getErrorOutput(): string;

    getOutput(): string;

    getCommand(): string;
}
```
***
##Интерфейс SqlBulkCopyBuilder:
```
interface SqlBulkCopyBuilder {
    /**
     * -S
     * @param value
     */
    setServerName(value: string): this;

    /**
     * Port is part of server name
     * @param value
     */
    setPort(value: number): this;

    /**
     * -U
     * @param value
     */
    setUsername(value: string): this;

    /**
     * -P
     * @param value
     */
    setPassword(value: string): this;

    /**
     * -d
     * @param value
     */
    setDatabase(value: string): this;

    /**
     * Query for export or table query string for import
     * @param value
     */
    setQuery(value: string): this;

    /**
     * -a
     * @param size
     */
    setPacketSize(size: number): this;

    /**
     * -b
     * @param size
     */
    setBatchSize(size: number): this;

    /**
     * -c
     * @param status
     */
    setCharacterTypesMode(status: boolean): this;

    /**
     * -C
     * @param code
     */
    setCodePage(code: string): this;

    /**
     * -D
     * @param status
     */
    setDsnMode(status: boolean): this;

    /**
     * -e
     * @param path
     */
    setErrorFile(path: string): this;

    /**
     * -E
     * @param status
     */
    setKeepIdentityValuesMode(status: boolean): this;

    /**
     * -f
     * @param path
     */
    setFormatFile(path: string): this;

    /**
     * -F
     * @param index
     */
    setFirstRow(index: number): this;

    /**
     * -h
     * @param hint
     */
    setHint(hint: string): this;

    /**
     * -i
     * @param path
     */
    setStandardInputFile(path: string): this;

    /**
     * -k
     * @param status
     */
    setKeepNullValuesMode(status: boolean): this;

    /**
     * -l
     * @param timeout
     */
    setLoginTimeout(timeout: number): this;

    /**
     * -L
     * @param index
     */
    setLastRow(index: number): this;

    /**
     * -m
     * @param size
     */
    setMaxErrors(size: number): this;

    /**
     * -n
     * @param status
     */
    setNativeTypesMode(status: boolean): this;

    /**
     * -N
     * @param status
     */
    setKeepNonTextNativeValuesMode(status: boolean): this;

    /**
     * -o
     * @param path
     */
    setOutputFile(path: string): this;

    /**
     * -q
     * @param status
     */
    setQuotedIdentifiersMode(status: boolean): this;

    /**
     * -r
     * @param term
     */
    setRowTerm(term: string): this;

    /**
     * -R
     * @param status
     */
    setRegionalMode(status: boolean): this;

    /**
     * -t
     * @param term
     */
    setFieldTerm(term: string): this;

    /**
     * -T
     * @param status
     */
    setTrustedConnectionMode(status: boolean): this;

    /**
     * -w
     * @param status
     */
    setWideCharacterTypesMode(status: boolean): this;

    import(path: string): SqlBulkCopyResult;

    export(path: string): SqlBulkCopyResult;

    /**
     * @param path
     * @param xml Default is true
     */
    format(path: string, xml: boolean): SqlBulkCopyResult;
}
```
***
##Mongodb и его интерфейсы:
```
declare namespace Mongodb {

    interface CollectionCreator {
        /**
         * https://docs.mongodb.com/manual/reference/method/db.createCollection
         * @param options
         */
        setOptions(options: {
            capped: boolean,
            autoIndexId: boolean,
            size: number,
            max: number
        }): CollectionCreator;

        setName(name: string): CollectionCreator;

        create(): { ok: number, errmsg?: string };
    }

    interface InsertOneResult {
        getInsertedCount(): number;

        getInsertedId(): Types.ObjectId;

        isAcknowledged(): boolean;
    }

    interface InsertManyResult {
        getInsertedCount(): number;

        getInsertedIds(): Types.ObjectId[];

        isAcknowledged(): boolean;
    }

    interface UpdateResult {
        getMatchedCount(): number;

        getModifiedCount(): number;

        getUpsertedCount(): number;

        getUpsertedId(): Types.ObjectId;

        isAcknowledged(): boolean;
    }

    interface DeleteResult {
        getDeletedCount(): number;

        isAcknowledged(): boolean;
    }

    interface Cursor {
        all(): object[];

        generator(): object[];
    }

    interface FilterOptions extends Object {
        sort: object,
        skip: number,
        limit: number,
        showRecordId: boolean,
        min: object,
        max: object
    }

    interface Collection {
        count(filter: object): number;

        find(filter: object, options?: FilterOptions): Cursor;

        findOne(filter: object, options?: FilterOptions): object;

        insertOne(document: object): InsertOneResult;

        insertMany(documents: object[]): InsertManyResult;

        updateOne(filter: object, update: object, options?: FilterOptions): UpdateResult;

        updateMany(filter: object, update: object, options?: FilterOptions): UpdateResult;

        deleteOne(filter: object, options?: FilterOptions): DeleteResult;

        deleteMany(filter: object, options?: FilterOptions): DeleteResult;
    }

    namespace Types {
        interface ObjectId {
            toString(): string;
        }
    }

    interface Types {
        objectId(id?: string): Types.ObjectId;

        regex(pattern: string, flags?: string): object;

        date(milliseconds: number): object;
    }

    interface Connection {
        collectionCreator(): CollectionCreator;

        dropCollection(name: string): { ok: number, errmsg?: string, nIndexesWas?: number, ns?: string };

        selectCollection(name: string): Collection;

        types(): Types;
    }

    interface ConnectorBuilder {
        setDSN(value: string): ConnectorBuilder;

        load(): Connection;
    }
}

```
***
##Http и его интерфейсы:
```
declare namespace Http {

    interface Params {
        getAll(): object;

        setAll(pairs: object): boolean;

        get(name: string): any;

        set(name: string, value: any): boolean;

        del(name: string): boolean;

        has(name: string): boolean;

        clear(): boolean;
    }

    interface UrlParams extends Params {
        stringify(): string;
    }

    interface JsonRequestBody {
        setJson(value: string | object): boolean;
    }

    interface StringRequestBody {
        setBody(value: string): boolean;
    }

    interface FormRequestBody {
        params(): Params;
    }

    interface RequestBody {
        /**
         * Content-Type: application/json
         */
        jsonBody(): JsonRequestBody;

        /**
         * Content-Type: application/x-www-form-urlencoded
         */
        formBody(): FormRequestBody;

        stringBody(): StringRequestBody;
    }

    interface Cert {
        setPath(path: string): Cert;

        getPath(path: string): string;

        setPassphrase(passphrase: string): Cert;
    }

    interface Url {
        setUrl(url: string): boolean;

        getUrl(): string;

        setUrlPath(path: string): boolean;

        getUrlPath(): string;

        getUrlScheme(): string;

        setUrlScheme(scheme: string): boolean;

        getHost(): string;

        setHost(host: string): boolean;

        getPort(): number | null;

        setPort(port: number | string): boolean;

        setUser(user: string): boolean;

        getUser(): string;

        setPassword(password: string): boolean;

        getPassword(): string | null;

        setFragment(fragment: string): boolean;

        getFragment(): string | null;

        params(): UrlParams;
    }

    interface AllowRedirects {
        setStatus(status: boolean): boolean;

        /**
         * Default is true
         */
        getStatus(): boolean;

        setMax(max: number): boolean;

        /**
         * Default is 5
         */
        getMax(): number;

        /**
         * This feature not realized
         */
        setStrict(strict: boolean): boolean;

        /**
         * Default is false
         */
        getStrict(): boolean;

        setWithReferer(withReferer: boolean): boolean;

        /**
         * Default is false
         */
        getWithReferer(): boolean;

        setProtocols(protocols: string[]): boolean;

        /**
         * Default is ["http", "https"]
         */
        getProtocols(): string[];
    }

    interface HttpAuth {
        setUser(user: string): HttpAuth;

        setPassword(password: string): HttpAuth;

        /**
         * @param type basic|digest|ntlm
         */
        setType(type: string): HttpAuth;

        setStatus(status: boolean): HttpAuth;
    }

    interface Options {
        setConnTimeout(seconds: number): boolean;

        getConnTimeout(): number;

        setReqTimeout(seconds: number): boolean;

        getReqTimeout(): number;

        setCanDecodeContent(value: boolean): boolean;

        getCanDecodeContent(): boolean;

        allowRedirects(): AllowRedirects;

        auth(): HttpAuth;

        /**
         * This feature not realized
         */
        cert(): Cert;

        verify(): Verify;
    }

    interface ResponseErrors {
        getCode(): number;

        getMessage(): string;
    }

    interface Response {
        headers(): ObjectOfStringArray;

        /**
         * Limit to first 50MB of response data
         */
        getStringData(): string;

        /**
         * Limit to parse first 50MB of response data
         */
        getStringDataLikeJson(): object | boolean;

        getStatusCode(): number;

        isOk(): boolean;

        getErrors(): ResponseErrors;
    }

    interface Verify {
        /**
         * Default is TRUE
         * @param value
         */
        setStatus(value: boolean): boolean;

        /**
         * This feature not realized
         */
        setPath(path: string): boolean;
    }

    interface RequestBuilder {
        url(): Url;

        /**
         *
         * @param type GET|POST|DELETE|PUT|HEAD|OPTIONS
         */
        setMethod(type: string): boolean;

        getMethod(): string;

        body(): RequestBody;

        options(): Options;

        cookies(): Params;

        headers(): Params;

        send(): Response;
    }

    interface HttpManager {
        requestBuilder(): RequestBuilder;

        urlEncode(value: string): string | boolean;

        urlDecode(value: string): string | boolean;

        base64Encode(value: string): string | boolean;

        base64Decode(value: string): string | boolean;
    }
}
```
***
##Интерфейс Connectors:
```
interface Connectors {
    mysql(): SqlConnectorBuilder;

    postgresql(): SqlConnectorBuilder;

    sqlServer(): SqlConnectorBuilder;

    oracle(): OracleConnectorBuilder;

    mongodb(): Mongodb.ConnectorBuilder;

    http(): Http.HttpManager;
}
```
***
##Интерфейс OM:
```
interface OM {
    readonly common: Common;
    readonly environment: Environment;
    readonly multicubes: Multicubes;
    readonly times: Times;
    readonly versions: Versions;
    readonly lists: Lists;
    readonly filesystems: Filesystems;
    readonly optimization: Optimization;
    readonly connectors: Connectors;
}
```
***

  
[Вернуться к содержанию](contents.md)

[Вернуться к оглавлению](index.md)