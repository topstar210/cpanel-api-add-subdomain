# cpanel-api-add-subdomain-
create subdomain with php script


// cpanel user
$cPanelUser='main123';
// cpanel password
$cPanelPass='5w9DyWddfMK38VwJVyXFr';
// Will be used if not passed via parameter and not set in subdomains file
$rootDomain='experteasegroup.com';
$subDomain='demo18';  

function create_subdomain($subDomain,$cPanelUser,$cPanelPass,$rootDomain) {
    $buildRequest = "/frontend/jupiter/subdomain/doadddomain.html?rootdomain=" . $rootDomain . "&domain=" . $subDomain . "&dir=developer";
    $openSocket = fsockopen('localhost',2082);
    if(!$openSocket) {
        return "Socket error";
        exit();
    }
    $authString = $cPanelUser . ":" . $cPanelPass;
    $authPass = base64_encode($authString);
    $buildHeaders  = "GET " . $buildRequest ."\r\n";
    $buildHeaders .= "HTTP/1.0\r\n";
    $buildHeaders .= "Host:localhost\r\n";
    $buildHeaders .= "Authorization: Basic " . $authPass . "\r\n";
    $buildHeaders .= "\r\n";
    fputs($openSocket, $buildHeaders);
    //while(!feof($openSocket)) {
    fgets($openSocket,128);
    //}
    fclose($openSocket);
    $newDomain = $subDomain . "." . $rootDomain;
    return $newDomain;
}

$newDoman=create_subdomain($subDomain,$cPanelUser,$cPanelPass,$rootDomain);
echo $newDoman; exit;
