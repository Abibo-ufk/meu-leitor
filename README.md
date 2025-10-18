# Leitor de Música para Android (Player)

Este é um projeto de um leitor de música completo para a plataforma Android, desenvolvido em Java.
A aplicação permite aos utilizadores gerir e ouvir as
suas músicas locais, criar e organizar playlists, e ainda inclui uma funcionalidade de reconhecimento de músicas semelhante ao Shazam.

## ✨ Funcionalidades Principais

*   **🎧 Leitor de Música:**
    *   Reprodução de ficheiros de áudio locais (`.mp3`, etc.).
    *   Controlos de reprodução: Play, Pause, Próximo e Anterior.
    *   Barra de progresso (SeekBar) para navegar na música.
    *   Modos Shuffle (aleatório) e Repeat (repetir).
    *   Animação de rotação da capa do álbum durante a reprodução.

*   **📚 Gestão de Biblioteca:**
    *   Scan automático do dispositivo para encontrar todos os ficheiros de áudio.
    *   Exibição da lista completa de músicas.
    *   Lista de reprodução "a tocar" visível na tela principal.

*   **🎶 Gestão de Playlists:**
    *   Criação, visualização e exclusão de playlists personalizadas.
    *   Adição de músicas da biblioteca a qualquer playlist.
    *   Remoção de músicas de uma playlist específica.
    *   Persistência de dados das playlists utilizando a base de dados **Room**.

*   **🎤 Reconhecimento de Música (Estilo Shazam):**
    *   Utiliza o microfone do dispositivo para capturar áudio ambiente.
    *   Integração com a API da **ACRCloud** para identificar o título e o artista da música a tocar.
    *   Pausa a reprodução local durante o reconhecimento e retoma-a automaticamente após o resultado.

*   **📱 Integração com o Sistema Android:**
    *   **Serviço em Primeiro Plano (`Foreground Service`):** A música continua a tocar mesmo com a aplicação em segundo plano ou com o ecrã desligado.
    *   **Notificação de Média:** Notificação persistente com controlos de reprodução (Play/Pause, Próximo, Anterior) e informações da faixa.
    *   Gestão de permissões de acesso a ficheiros de áudio e gravação de áudio em versões recentes do Android (API 33+).

## 🏗️ Arquitetura do Projeto

O projeto segue a arquitetura **Model-View-Presenter (MVP)**, que ajuda a separar as responsabilidades e a tornar o código mais organizado, testável e manutenível.

*   **Model:** Representa os dados e a lógica de negócio.
    *   `Musica.java`: Objeto que representa uma faixa de áudio.
    *   `Playlist.java`, `Song.java`: Entidades da base de dados **Room** para persistir as playlists.
    *   `PlaylistRepository.java`: Abstrai o acesso aos dados, comunicando com o Room.
    *   `AudioRecognizer.java`: Encapsula a lógica de comunicação com a API da ACRCloud.

*   **View:** A camada de interface do utilizador (UI). É "passiva" e apenas exibe os dados e reporta as interações do utilizador ao Presenter.
    *   `MainActivity.java`: Ecrã principal do leitor de música.
    *   `PlaylistActivity.java`: Ecrã que lista todas as playlists criadas.
    *   `PlaylistDetailsActivity.java`: Ecrã que mostra as músicas de uma playlist.
    *   `MusicAdapter.java`, `PlaylistAdapter.java`: Adaptadores para as `RecyclerViews`.

*   **Presenter:** Atua como um intermediário entre a View e o Model.
    *   `presenter.java`: Contém toda a lógica de apresentação. Recebe os eventos da View, interage com o Model (`MusicService`, `PlaylistRepository`) e atualiza a View com os novos dados.
    *   `MusicContract.java`: Define a interface de comunicação entre a View e o Presenter.

*   **Service:**
    *   `MusicService.java`: Componente central que gere o `ExoPlayer` e a `MediaSession`, permitindo que a música toque em segundo plano.

## 🛠️ Dependências Utilizadas

*   **AndroidX Libraries**: `appcompat`, `recyclerview`, `constraintlayout`.
*   **Material Components**: Para um design moderno e componentes de UI como o `FloatingActionButton`.
*   **Media3 ExoPlayer**: A biblioteca recomendada pelo Google para reprodução de áudio e vídeo.
*   **Room Persistence Library**: Para a gestão da base de dados local onde as playlists são guardadas.
*   **ACRCloud SDK**: Biblioteca externa para a funcionalidade de reconhecimento de música.

## 🚀 Como Configurar e Executar

1.  **Clonar o Repositório:**
    