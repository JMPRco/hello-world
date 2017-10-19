function sendemail($fromemail, $fromname, $toemail, $toname, $subject, $message) {
date_default_timezone_set("Europe/Moscow"); // устанавливаем часовую зону
require "PHPMailerAutoload.php"; // подключаем файл автозагрузки
$mail = new PHPMailer(); // инициализируем класс
file_exists("/language/phpmailer.lang-ru.php") ? $mail->SetLanguage("ru", "/language/") : $mail->SetLanguage("en", /language/"); // подключили языковой пакет для вывода ошибок и отчетов
$mail->isMAIL(); // указали, что не смтп
$mail->CharSet = "UTF-8"; // кодировка заголовков
$mail->setFrom($fromemail, $fromname); // от кого
$mail->addReplyTo($fromemail, $fromname); // адрес и имя для ответа
$mail->Subject = $subject; // заголовок письма (тема сообщения)
$plain = $mail->html2text($message); // создаем текстовую версию для устройств, не поддерживающих html
$mail->isHTML(true); // указали, что сообщение в стандарте html
$img_path = "/images/mylogo.png"; // адрес логотипа
$img_cid = md5($img_path); // сид логотипа
$img_name = "mylogo"; // имя логотипа
$mail->addEmbeddedImage($img_path, $img_cid, $img_name); // добавили в тело письма логотип
$body = "<!DOCTYPE html>"; // создаем тело письма
$body .= "<html><head>"; // структуру я минимизирую, шаблонов в сети много, либо создайте свой
$body .= "<meta charset='UTF-8' />";
$body .= "<title>".$subject."</title>";
$body .= "</head><body>";
$body .= "<table><tr><td>";
$body .= "<table style='width:600px'><tr><td>";
$body .= "<a href='http://www.meweb.ru/' title='MeWEB' target='_blank'><img src='cid:".$img_cid."' alt='MeWEB' /></a></td>"; // указали место, где будет отображен логотип
$body .= "<td>";
$body .= "<a href='http://www.meweb.ru/' title='MeWEB' target='_blank'>MeWEB</a><br /><br /><a href='mailto:".$fromemail."'>".$fromemail."</a></td></tr>";
$body .= "<tr><td colspan='2'>&nbsp;</td></tr>";
$body .= "<tr><td colspan='2'><h3 syle='text-align:center'>".$subject."</h3>".nl2br($message)."</td></tr>"; // вывели в тело тему письма и само письмо
$body .= "<tr><td colspan='2'><em>All rights reserved | Copyright &copy; <a href='http://www.meweb.ru/' title='MeWEB' target='_blank'>MeWEB</a> ".date("Y")."</em></td></tr>";
$body .= "</table></td></tr></table>";
$body .= "</body></html>";
$mail->msgHTML($body); // формируем тело
$mail->AltBody = $plain; // альтернативное тело письма
$mail->addAddress($toemail, $toname); // добавляем получателя и отправляем
if (!$mail->send()) { // если произошла ошибка при отправке
$return = $toname." | ".str_replace("@", "&#64;", $toemail)." ".$mail->ErrorInfo."  | ".date("d-m-Y в H:i:s"); // возвращаем сообщение об ошибке
} else {
$return = $toname." | ".str_replace("@", "&#64;", $toemail)." | ".date("d-m-Y в H:i:s");
} // если сообщение отправлено удачно- возвращаем время отправки
$mail->clearAddresses();
$mail->clearCustomHeaders();
$mail->clearAttachments();
$mail->clearReplyTos(); // чистим все заголовки
return $return;
}
